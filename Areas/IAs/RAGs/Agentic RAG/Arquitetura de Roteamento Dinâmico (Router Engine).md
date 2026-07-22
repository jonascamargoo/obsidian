---
tipo: conceito
area: IAs
tags:
- ia/rag
- ia/agentes
criada: '2026-04-20'
---

## 1. O Padrão Router em Agentic RAG

O roteamento (Routing) é a forma mais elementar de raciocínio agentic. Em vez de forçar todas as queries por um único funil de busca vetorial (Vector Search), o sistema delega a um LLM a decisão de qual motor de busca (Query Engine) é algoritmicamente mais adequado para resolver a intenção da query.

### Por que usar um Router?

- **Otimização de Contexto:** Consultas de sumarização exigem a injeção de todo o documento no contexto, enquanto consultas de fatos exigem apenas _Top-K_ chunks.
    
- **Desacoplamento:** Permite escalar o sistema acoplando diferentes fontes de dados (ex: SQL, APIs, Vetores) sob uma interface de entrada única.
    

---

## 2. Pipeline de Ingestão e Indexação Dupla

Um conceito arquitetônico fundamental em LlamaIndex é que **Nodes (chunks) podem ser indexados de múltiplas formas simultaneamente**, alterando drasticamente o comportamento de recuperação (retrieval).

### Ingestão e Chunking

O documento é transformado em uma representação de grafo de nós (`nodes`).



```Python
# Estratégia de particionamento baseada em sentenças para preservar integridade semântica
splitter = SentenceSplitter(chunk_size=1024)
nodes = splitter.get_nodes_from_documents(documents)
```

### Estratégias de Indexação Contrastantes

Instanciamos dois índices sobre o mesmo conjunto de dados (`nodes`):

1. **`VectorStoreIndex`:**
    
    - **Mecanismo:** Calcula o _embedding_ de cada nó (usando `text-embedding-ada-002`) e realiza busca de similaridade (Cosine/Euclidean) no espaço latente.
        
    - **Caso de uso:** Recuperação de contexto específico (Ex: _"Como os agentes compartilham informações?"_).
        
2. **`SummaryIndex`:**
    
    - **Mecanismo:** Um índice determinístico que ignora a similaridade semântica. Quando consultado, ele recupera **todos os nós** contidos no índice.
        
    - **Caso de uso:** Síntese e sumarização global (Ex: _"Qual o resumo do documento?"_).
        
![[Pasted image 20260416150944.png]]
---

## 3. Abstração de Ferramentas (Tools) e Metadados

Para que o LLM atue como um roteador de forma determinística, as instâncias de `QueryEngine` precisam ser envelopadas em uma abstração de "Ferramenta" (`QueryEngineTool`).

**A engenharia de prompt aqui ocorre nos metadados da ferramenta:** A `description` atua como a heurística de decisão para o LLM. É crucial ser explícito e mutuamente excludente nas descrições.

```Python
summary_tool = QueryEngineTool.from_defaults(
    query_engine=summary_query_engine,
    description="Useful for summarization questions related to MetaGPT"
)

vector_tool = QueryEngineTool.from_defaults(
    query_engine=vector_query_engine,
    description="Useful for retrieving specific context from the MetaGPT paper."
)
```

> [!NOTE] Assincronismo e Sumarização Para o `summary_query_engine`, o modo `response_mode="tree_summarize"` é ativado com `use_async=True`. Como a sumarização exige processar _todos_ os chunks (34 chunks no caso do MetaGPT), o LlamaIndex monta uma árvore hierárquica de prompts. A execução assíncrona permite processar folhas dessa árvore em paralelo, reduzindo drasticamente a latência da API de inferência. (Nota de infraestrutura: exige o uso de `nest_asyncio` em ambientes Jupyter para não bloquear o _Event Loop_ principal).

---

## 4. Mecanismos de Seleção (Selectors)

O núcleo lógico do `RouterQueryEngine` é o seu _Selector_. O framework fornece diferentes implementações para garantir robustez:

- **`LLMSingleSelector` (Utilizado na lição):** Pede ao LLM para analisar as descrições das ferramentas e gerar um JSON cru com a ferramenta escolhida. O LlamaIndex faz o _parsing_ do JSON e executa a chamada.
    
- **Pydantic Selectors (Recomendado para Produção):** Em vez de depender do _parsing_ de JSON textual, utiliza as APIs de _Function Calling_ nativas (como as da OpenAI). O LLM é forçado a retornar um schema Pydantic estrito, eliminando falhas de _parsing_ e alucinação de argumentos.
    

```python
# Instanciação do Roteador
query_engine = RouterQueryEngine(
    selector=LLMSingleSelector.from_defaults(),
    query_engine_tools=[summary_tool, vector_tool],
    verbose=True # Essencial para observabilidade do "pensamento" (tracing)
)
```

---

## 5. Inspeção de Estado e Observabilidade

Para debugar decisões de roteamento, o engenheiro deve avaliar a propriedade `source_nodes` da resposta.

- **Validação de Sumarização:** Se a query foi _"Qual o resumo do documento?"_, o roteador deve selecionar o `summary_tool`. A asserção `len(response.source_nodes) == 34` confirma que o motor ignorou a busca vetorial e ejetou todo o dataset no pipeline de `tree_summarize`.
    
- **Validação de Vetorização:** Em uma query pontual (_"Tell me about the ablation study results"_), o log `verbose=True` mostrará `Selecting query engine 1` (Vector Tool), e o payload de `source_nodes` retornará apenas o _Top-K_ padrão (geralmente k=2).