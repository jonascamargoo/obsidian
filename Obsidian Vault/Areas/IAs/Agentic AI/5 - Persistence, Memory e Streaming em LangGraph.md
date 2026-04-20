## 1. O Problema do Estado Volátil

Em agentes básicos (como na Lição 1), a memória reside inteiramente na RAM da aplicação (uma lista de mensagens em escopo de execução). Em um ambiente de produção (_LLMOps_), onde múltiplas instâncias da aplicação lidam com milhares de usuários simultâneos, essa abordagem falha. Se o processo morre, o histórico é perdido; se a tarefa é de longa duração (assíncrona), a thread principal fica bloqueada.

Para resolver isso, o LangGraph introduz a abstração de **Checkpointer**.

### O Componente Checkpointer

O _Checkpointer_ age como uma camada de persistência de banco de dados nativamente integrada ao ciclo de vida do grafo. Ele serializa e salva o estado do agente (o `AgentState` e suas mensagens) **após a execução de cada nó**.

- **Implementações:** Para desenvolvimento local, usa-se o `SqliteSaver` (frequentemente em memória `:memory:`). Para produção, o framework suporta adaptadores para Redis, PostgreSQL, entre outros.
    
- **Injeção de Dependência:** O _checkpointer_ é anexado ao grafo no momento de sua compilação, tornando a camada de banco de dados invisível para a lógica de roteamento dos nós.
    

```Python
from langgraph.checkpoint.sqlite import SqliteSaver

memory = SqliteSaver.from_conn_string(":memory:")
self.graph = graph.compile(checkpointer=memory) # O grafo agora é stateful
```

---

## 2. Orquestração de Sessões Paralelas (`thread_id`)

Com a persistência habilitada, o grafo precisa de uma chave primária para saber qual estado recuperar do banco de dados antes de invocar o LLM. Isso é feito através do parâmetro `thread_config`.

```Python
thread = {"configurable": {"thread_id": "1"}}

# Primeira iteração
for event in abot.graph.stream({"messages": [HumanMessage("What is the weather in SF?")]}, thread):
    pass

# Segunda iteração (Follow-up) - O agente lembra do contexto devido ao thread_id
for event in abot.graph.stream({"messages": [HumanMessage("What about in LA?")]}, thread):
    pass
```

**Análise de Falha de Contexto:** Se alterarmos o `thread_id` para `"2"` e perguntarmos _"Which one is warmer?"_, a query falha. O LangGraph inicializa um novo escopo de estado no SQLite, e o LLM perde a referência anafórica ("Which one").

---

## 3. Arquitetura de Observabilidade: Streaming de Eventos

Processos _agentic_ podem levar dezenas de segundos para resolver queries complexas devido a múltiplos _round-trips_ de ferramentas. Para garantir uma boa UX e facilitar o _debugging_, o LangGraph expõe _streams_ de dados.

### Nível 1: Streaming de Mutação de Estado (Messages)

Ao substituir `graph.invoke()` por `graph.stream()`, a função se torna um gerador que emite eventos (_yield_) a cada vez que um nó conclui sua execução e atualiza o `AgentState`.

- O cliente recebe os eventos na exata ordem do _Reasoning Loop_:
    
    1. O LLM gera a intenção (`tool_calls`).
        
    2. O nó de Ação executa e injeta a `ToolMessage` (Observação).
        
    3. O LLM avalia a observação e gera a resposta final.
        

---

## 4. Streaming Assíncrono de Tokens (Real-time UX)

Para simular o efeito de digitação em tempo real (como no ChatGPT), precisamos descer um nível na abstração e observar os tokens individuais gerados pela API do LLM, não apenas as mensagens consolidadas.

### Engenharia de IO Assíncrono

Streaming de tokens exige que a aplicação inteira adote o _Event Loop_ assíncrono do Python (`asyncio`). Consequentemente, o banco de dados também não pode ser bloqueante.

1. **Troca de Infraestrutura:** Substituímos `SqliteSaver` por `AsyncSqliteSaver`.
    
2. **API de Eventos Estendida:** Utilizamos `.astream_events()` especificando a versão da API do LangChain (`version="v1"`).
    
3. **Filtragem de Topologia (`on_chat_model_stream`):** O barramento de eventos emite informações de todos os nós (LLM, ferramentas, roteadores). Precisamos filtrar especificamente os eventos onde o nó do modelo de linguagem está ejetando _chunks_.
    

```Python
from langgraph.checkpoint.aiosqlite import AsyncSqliteSaver
memory = AsyncSqliteSaver.from_conn_string(":memory:")

# ... setup do agente assíncrono ...

async for event in abot.graph.astream_events({"messages": messages}, thread, version="v1"):
    if event["event"] == "on_chat_model_stream":
        content = event["data"]["chunk"].content
        if content:
            print(content, end="|")
```

> [!IMPORTANT] O Comportamento do Payload de Function Calling Se o desenvolvedor observar os chunks emitidos e notar a ausência de `content` (string vazia), isso não é um bug. No protocolo da OpenAI, quando o LLM decide invocar uma ferramenta, ele para de emitir o atributo `content` e passa a preencher um atributo oculto no chunk contendo o _JSON Schema_ dos argumentos da função. O código de produção deve tratar silenciosamente chunks onde `if not content:` para evitar renderização de artefatos na UI.

---

## Notebook

```python
# Lesson 4: Persistence and Streaming[](https://s172-29-30-111p8888.lab-aws-production.deeplearning.ai/notebooks/L4/Lesson_4_Student.ipynb#Lesson-4:-Persistence-and-Streaming)

from dotenv import load_dotenv

​

_ = load_dotenv()

from langgraph.graph import StateGraph, END

from typing import TypedDict, Annotated

import operator

from langchain_core.messages import AnyMessage, SystemMessage, HumanMessage, ToolMessage

from langchain_openai import ChatOpenAI

from langchain_community.tools.tavily_search import TavilySearchResults

tool = TavilySearchResults(max_results=2)

class AgentState(TypedDict):

    messages: Annotated[list[AnyMessage], operator.add]

from langgraph.checkpoint.sqlite import SqliteSaver

​

memory = SqliteSaver.from_conn_string(":memory:")

class Agent:

    def __init__(self, model, tools, checkpointer, system=""):

        self.system = system

        graph = StateGraph(AgentState)

        graph.add_node("llm", self.call_openai)

        graph.add_node("action", self.take_action)

        graph.add_conditional_edges("llm", self.exists_action, {True: "action", False: END})

        graph.add_edge("action", "llm")

        graph.set_entry_point("llm")

        self.graph = graph.compile(checkpointer=checkpointer)

        self.tools = {t.name: t for t in tools}

        self.model = model.bind_tools(tools)

​

    def call_openai(self, state: AgentState):

        messages = state['messages']

        if self.system:

            messages = [SystemMessage(content=self.system)] + messages

        message = self.model.invoke(messages)

        return {'messages': [message]}

​

    def exists_action(self, state: AgentState):

        result = state['messages'][-1]

        return len(result.tool_calls) > 0

​

    def take_action(self, state: AgentState):

        tool_calls = state['messages'][-1].tool_calls

        results = []

        for t in tool_calls:

            print(f"Calling: {t}")

            result = self.tools[t['name']].invoke(t['args'])

            results.append(ToolMessage(tool_call_id=t['id'], name=t['name'], content=str(result)))

        print("Back to the model!")

        return {'messages': results}

prompt = """You are a smart research assistant. Use the search engine to look up information. \

You are allowed to make multiple calls (either together or in sequence). \

Only look up information when you are sure of what you want. \

If you need to look up some information before asking a follow up question, you are allowed to do that!

"""

model = ChatOpenAI(model="gpt-4o")

abot = Agent(model, [tool], system=prompt, checkpointer=memory)

messages = [HumanMessage(content="What is the weather in sf?")]

thread = {"configurable": {"thread_id": "1"}}

for event in abot.graph.stream({"messages": messages}, thread):

    for v in event.values():

        print(v['messages'])

messages = [HumanMessage(content="What about in la?")]

thread = {"configurable": {"thread_id": "1"}}

for event in abot.graph.stream({"messages": messages}, thread):

    for v in event.values():

        print(v)

messages = [HumanMessage(content="Which one is warmer?")]

thread = {"configurable": {"thread_id": "1"}}

for event in abot.graph.stream({"messages": messages}, thread):

    for v in event.values():

        print(v)

messages = [HumanMessage(content="Which one is warmer?")]

thread = {"configurable": {"thread_id": "2"}}

for event in abot.graph.stream({"messages": messages}, thread):

    for v in event.values():

        print(v)

## Streaming tokens[](https://s172-29-30-111p8888.lab-aws-production.deeplearning.ai/notebooks/L4/Lesson_4_Student.ipynb#Streaming-tokens)

from langgraph.checkpoint.aiosqlite import AsyncSqliteSaver

​

memory = AsyncSqliteSaver.from_conn_string(":memory:")

abot = Agent(model, [tool], system=prompt, checkpointer=memory)

messages = [HumanMessage(content="What is the weather in SF?")]

thread = {"configurable": {"thread_id": "4"}}

async for event in abot.graph.astream_events({"messages": messages}, thread, version="v1"):

    kind = event["event"]

    if kind == "on_chat_model_stream":

        content = event["data"]["chunk"].content

        if content:

            # Empty content in the context of OpenAI means

            # that the model is asking for a tool to be invoked.

            # So we only print non-empty content

            print(content, end="|")

​

```


### Tags & Referências

- #LangGraph #Persistence #StateManagement #AsyncIO #EventStreaming #LLMOps #Checkpointer