## 1. Escalonamento Inicial: Agentes Multi-Documento (Small Scale)

Para expandir um agente RAG de um único documento para múltiplos documentos, a abordagem inicial (ingênua) consiste em instanciar o par de ferramentas padrão (`VectorTool` e `SummaryTool`) para cada documento e injetar todas em uma lista plana no prompt do agente.
![[Pasted image 20260416162543.png]]

- **Matemática do Escalonamento:** Para $N$ documentos, o agente recebe $2N$ ferramentas em seu inventário.
    
- **Comportamento:** O LLM analisa o JSON Schema de todas as $2N$ ferramentas a cada iteração do seu _Reasoning Loop_ para decidir qual chamar. Isso permite raciocínio cruzado (Ex: _"Compare a abordagem do documento A com o documento B"_), pois o agente pode encadear chamadas ao `SummaryTool(A)` e depois ao `SummaryTool(B)`.
    
![[Pasted image 20260416162957.png]]
---

## 2. O Gargalo de Produção: "Tool Stuffing"

A abordagem de lista plana quebra rapidamente ao escalar de 3 documentos (6 ferramentas) para 11 documentos (22 ferramentas) ou centenas. Injetar todas as assinaturas de funções no prompt do LLM gera três degradações críticas no sistema:

1. **Context Window Overflow:** As descrições e schemas das ferramentas estouram o limite de tokens do modelo.
    
2. **Degradação de Roteamento (LLM Confusion):** Aumentar o espaço de busca de funções diminui a precisão da inferência. O LLM sofre de "paralisia de análise" e falha em escolher a ferramenta correta entre opções semanticamente próximas.
    
3. **Explosão de Custo e Latência:** O _overhead_ de tokens de input cresce linearmente a cada turno conversacional.
    

---

## 3. A Solução Arquitetural: Tool Retrieval (Meta-RAG)

Para resolver o _Tool Stuffing_, aplicamos os princípios de Recuperação Aumentada (RAG) **ao próprio inventário de ferramentas**, e não apenas aos textos. Em vez de passar o inventário completo, passamos apenas as _Top-K_ ferramentas mais relevantes para a intenção atual.

### Como funciona o Tool Retrieval:

1. **Vetorização de Ferramentas:** Em vez de vetorizar parágrafos de texto, vetorizamos a `description` e os metadados de cada `FunctionTool`.
    
2. **Busca Semântica Dinâmica:** Quando o usuário faz uma query, o motor busca no espaço vetorial quais ferramentas têm o escopo semântico mais alinhado com a pergunta.
    
3. **Injeção Dinâmica (Prompting):** Apenas as ferramentas recuperadas (ex: `top_k=3`) são injetadas no prompt do _Agent Worker_ para aquela iteração específica.
    

---

## 4. Implementação no LlamaIndex (`ObjectIndex`)

O LlamaIndex introduz a abstração `ObjectIndex` para lidar com a serialização e busca vetorial de objetos Python arbitrários (neste caso, instâncias de `QueryEngineTool`).

### Pipeline de Indexação de Objetos

```Python
from llama_index.core.objects import ObjectIndex
from llama_index.core import VectorStoreIndex

# 1. Criação do índice de ferramentas (serialização de Python Objects para Vectors)
obj_index = ObjectIndex.from_objects(
    all_tools, # Lista com dezenas/centenas de ferramentas
    index_cls=VectorStoreIndex,
)

# 2. Definição do Recuperador de Ferramentas
obj_retriever = obj_index.as_retriever(similarity_top_k=3)
```

_A engenharia por trás do `ObjectIndex`:_ Ele mantém um mapeamento em memória ou no banco de dados entre o embedding gerado (a partir da docstring da ferramenta) e o ponteiro para o objeto Python executável.

### Orquestração com o Agente

Na instanciação do _Worker_, substituímos o argumento estático `tools` pelo injetor dinâmico `tool_retriever`. Adicionalmente, injetamos um `system_prompt` rigoroso para evitar que o LLM alucine respostas usando conhecimento paramétrico pré-treinado, forçando a dependência nas ferramentas recuperadas.

```Python
agent_worker = FunctionCallingAgentWorker.from_tools(
    tool_retriever=obj_retriever, # Substitui a lista estática
    llm=llm, 
    system_prompt="""
    You are an agent designed to answer queries over a set of given papers.
    Please always use the tools provided to answer a question. Do not rely on prior knowledge.
    """,
    verbose=True
)
```

---

## 5. Fluxo de Execução Otimizado (Trace Analysis)

Para uma query como _"Compare o LoftQ com o LongLora"_, o pipeline executa na seguinte ordem:

1. **Tool Retrieval:** O `obj_retriever` vetoriza a query e recupera as ferramentas `summary_tool_loftq` e `summary_tool_longlora`.
    
2. **Agent Reasoning (Passo 1):** O LLM (agora ciente apenas dessas duas ferramentas) decide invocar `summary_tool_loftq`.
    
3. **Agent Reasoning (Passo 2):** O LLM invoca `summary_tool_longlora`.
    
4. **Síntese Final:** O LLM compara os _outputs_ em memória e gera a resposta final.
    

O contexto do LLM permaneceu limpo, processando apenas os metadados de 2 a 3 ferramentas, otimizando o _recall_ e a latência da API.

---

### Tags & Referências

- #AgenticRAG #ToolRetrieval #ObjectIndex #MultiDocumentRAG #PromptOptimization #LlamaIndex #VectorSearch