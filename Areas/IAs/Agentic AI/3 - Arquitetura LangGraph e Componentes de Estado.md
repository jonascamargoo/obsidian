---
tipo: aula
area: IAs
tags:
- ia/agentes
criada: '2026-04-20'
---

## 1. Do "While Loop" para a Máquina de Estados (State Machine)

### Como foi feito antes (forma "ruim")
![[Pasted image 20260417173306.png]]

### LangGraph

A implementação _from scratch_ da lição anterior utilizava um loop `while` acoplado a um parsing frágil de Regex. O LangGraph formaliza esse processo utilizando os conceitos da Teoria dos Grafos para construir Máquinas de Estado Finito.

**Conceitos Core do LangGraph:**

1. **Nodes (Nós):** Executores funcionais. Geralmente representam uma chamada ao LLM ou a execução de uma ferramenta (Python).
    
2. **Edges (Arestas):** O fluxo fixo. Conecta garantidamente o nó A ao nó B.
    
3. **Conditional Edges (Arestas Condicionais):** O roteamento dinâmico. Avalia o estado atual do agente e decide qual caminho o grafo deve seguir (ex: `if tool_call -> Node(Action)` ou `if done -> END`).
    
4. **Agent State (Estado do Agente):** O contexto global que é passado e mutado de nó em nó.

---

## 2. Modelagem do Estado (`AgentState`)

Diferente do LangChain padrão que sobrescreve variáveis de contexto, o LangGraph utiliza tipagem em Python (`TypedDict`) e anotações (`Annotated`) para definir **como** o estado deve ser atualizado durante o ciclo de vida do grafo.

```Python
from typing import TypedDict, Annotated
import operator
from langchain_core.messages import AnyMessage

class AgentState(TypedDict):
    # O operator.add indica um Reducer. Novos dados são apensados (append), não substituídos.
    messages: Annotated[list[AnyMessage], operator.add]
```

- **A Matemática do Estado:** A escolha do reducer `operator.add` é vital para a memória conversacional. Quando o nó _Action_ retorna um `ToolMessage`, o LangGraph não apaga a memória do LLM; ele _anexa_ a observação à lista, preservando o histórico completo (Lineage) do raciocínio.
---

## 3. Arquitetura da Classe `Agent` no LangGraph

A reconstrução do nosso agente envolve três componentes metodológicos principais na nossa classe `Agent`:

### A. O Nó do LLM (`call_openai`)

Prepara as mensagens, injeta o _System Prompt_ e chama a API.

- **Binding de Ferramentas:** Utilizamos `model.bind_tools(tools)`. Diferente da lição 1 (onde descrevíamos ferramentas por texto), isso aciona a API nativa de _Function Calling_ (JSON Schema) da OpenAI, garantindo que o modelo retorne atributos estruturados (`tool_calls`) em vez de strings parseáveis por Regex.
    

### B. A Aresta Condicional (`exists_action`)

Avaliador lógico simples que define a topologia do grafo em tempo de execução.

```Python
def exists_action(self, state: AgentState):
    result = state['messages'][-1] # Pega a última mensagem (gerada pelo LLM)
    return len(result.tool_calls) > 0 # Retorna True se o LLM decidiu usar uma ferramenta
```

### C. O Nó de Ação (`take_action`) e Parallel Tool Calling

Responsável por executar a ferramenta externa (ex: Tavily Search) com os argumentos definidos pelo LLM.

- **Resiliência:** A implementação verifica se o modelo "alucinou" um nome de ferramenta inválido. Em vez de quebrar a aplicação (Exception), ele instrui o LLM a tentar novamente (`bad tool name, retry`).
    
- **Parallel Calling:** A iteração `for t in tool_calls:` suporta instâncias em que o LLM (como o GPT-4o) decide executar múltiplas buscas assíncronas simultaneamente (ex: _"Clima em SF e LA"_, acionando duas chamadas `Tavily` de uma só vez, reduzindo latência em $50\%$).
    

---

## 4. Construção e Compilação do Grafo

O construtor da classe (`__init__`) "plumba" (conecta) os nós e arestas descritos acima.

Python

```
graph = StateGraph(AgentState)

# 1. Definição dos Nós
graph.add_node("llm", self.call_openai)
graph.add_node("action", self.take_action)

# 2. Definição do Roteamento
graph.add_conditional_edges(
    "llm",                  # Nó de origem
    self.exists_action,     # Função avaliadora (Router)
    {True: "action", False: END} # Mapa de transição
)
graph.add_edge("action", "llm") # O loop de volta (Ação -> Raciocínio)

# 3. Entrypoint e Compilação
graph.set_entry_point("llm")
self.graph = graph.compile() # Retorna um Langchain Runnable interface (.invoke())
```

> [!NOTE] Compilação vs Interpretação
> 
> `graph.compile()` "congela" a arquitetura do grafo. Ele fornece o ambiente de execução e prepara os _checkpoints_ de estado que permitirão persistência e _Human-in-the-loop_ (funcionalidades das próximas aulas).

---

## 5. Raciocínio Sequencial vs. Paralelo (Trace Analysis)

Ao testar o grafo com a _Tavily Search_, observamos diferentes níveis de complexidade de raciocínio da engine do LLM:

- **Grau 1 (Raciocínio Simples):** _"Clima em SF"_. O LLM mapeia a intenção, invoca 1 ferramenta, recebe a `ToolMessage` e encerra `(False -> END)`.
    
- **Grau 2 (Raciocínio Paralelo):** _"Clima em SF e LA"_. O modelo compila as duas intenções imediatamente (`tool_calls` length = 2). As duas requisições à Tavily ocorrem no mesmo loop, e o resultado consolida-se em um único _return_.
    
- **Grau 3 (Raciocínio Sequencial / CoT):** _"Quem ganhou o Super Bowl de 2024? Qual o PIB do estado da sede desse time?"_. O modelo **não pode** paralelizar. Ele precisa invocar a busca 1, pausar `(PAUSE/LLM node -> Action node)`, esperar a Observação (que o time é o Chiefs, com sede no Missouri), e no próximo ciclo lógico `(Action node -> LLM node)`, disparar a busca 2 (PIB do Missouri). Isso prova a funcionalidade crítica da aresta de retorno cíclica do LangGraph.
    

---

### Tags & Referências

- #LangGraph #StateGraph #FunctionCalling #AgenticDesign #TavilySearch #ParallelToolCalling #LLMArchitecture