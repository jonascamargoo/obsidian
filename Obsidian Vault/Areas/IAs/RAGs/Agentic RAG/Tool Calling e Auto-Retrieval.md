
## 1. O Paradigma de Tool Calling em RAG

Em um pipeline RAG padrão, o LLM é relegado a um papel passivo de sintetizador de texto (lendo contextos injetados). A transição arquitetônica da Lição 1 (Roteamento) para a Lição 2 (Tool Calling) representa a mudança para um estado ativo: o LLM interage com o ambiente externo.

Enquanto um **Router** apenas seleciona qual motor de busca usar (escolha discreta), o **Tool Calling** permite que o LLM:

1. Selecione a ferramenta (função) apropriada.
    
2. **Infira e estruture os argumentos (parâmetros)** necessários para executar essa função com base na intenção do usuário.
    

---

## 2. Abstração de Funções Nativas (`FunctionTool`)

O LlamaIndex fornece a classe `FunctionTool` para encapsular qualquer função Python arbitrária em uma interface compreensível para o LLM. O framework integra-se nativamente com as APIs de _Function Calling_ (como as da OpenAI).

### A Engenharia por trás do Encapsulamento

O processo de envelopamento não é apenas estrutural; ele compila a assinatura da função em um _JSON Schema_ que o LLM consome. Portanto, a qualidade da inferência depende estritamente das boas práticas de engenharia de software na definição da função:


```Python
from llama_index.core.tools import FunctionTool

def vector_query(query: str, page_numbers: List[str]) -> str:
    """Perform a vector search over an index.
    
    query (str): the string query to be embedded.
    page_numbers (List[str]): Filter by set of pages. Leave BLANK if we want to perform a vector search over all pages.
    """
    # ... implementação ...
```

**O que é extraído para o Prompt/Schema do LLM?**

- **Type Hints (`str`, `List[str]`):** Definem os tipos de dados esperados no payload JSON retornado pelo LLM.
    
- **Docstrings:** Atuam como a "instrução de sistema" para aquela ferramenta, detalhando o comportamento esperado e as condições de borda (ex: _Leave BLANK se não houver página explícita_).
    

---

## 3. Auto-Retrieval e Filtros de Metadados Dinâmicos

Um dos problemas clássicos do _Naive RAG_ é a perda de precisão em repositórios muito grandes devido a colisões no espaço vetorial. O padrão de **Auto-Retrieval** resolve isso combinando busca semântica com **pré-filtragem exata (metadata filtering)**.

### Propagação de Metadados nos Nós (Nodes)

Durante a ingestão (`SimpleDirectoryReader`), cada nó/chunk herda metadados do documento original (ex: `page_label`, `file_name`, datas). Você pode inspecionar o grafo de nós habilitando `metadata_mode="all"`, que revela que o LlamaIndex anexa o cabeçalho de metadados diretamente no payload de texto.

### Implementação do Auto-Retrieval

Em vez de pedir para o usuário definir filtros na interface (UI), delegamos isso ao LLM. Criamos uma função de busca que aceita uma lista de páginas como argumento.


```Python
from llama_index.core.vector_stores import MetadataFilters, FilterCondition

# Dentro da função vector_query...
metadata_dicts = [
    {"key": "page_label", "value": p} for p in page_numbers
]

query_engine = vector_index.as_query_engine(
    similarity_top_k=2,
    filters=MetadataFilters.from_dicts(
        metadata_dicts,
        condition=FilterCondition.OR # Aplica OR lógico entre as páginas solicitadas
    )
)
```

**Fluxo de Execução Oculto:**

1. **Query do Usuário:** _"What are the high-level results of MetaGPT as described on page 2?"_
    
2. **LLM Inference:** O modelo extrai `query="high-level results of MetaGPT"` e `page_numbers=["2"]`.
    
3. **Execução:** O Vector Store aplica um filtro exato (WHERE page_label = '2') no banco de dados vetorial antes de realizar o cálculo de similaridade de cossenos (K-NN). Isso garante precisão absoluta na restrição de escopo e economiza computação de busca.
    

---

## 4. Orquestração Multi-Tool (`predict_and_call`)

A interface para invocar o LLM com um arsenal de ferramentas é o método `predict_and_call`.


```Python
response = llm.predict_and_call(
    [vector_query_tool, summary_tool], 
    "What are the MetaGPT comparisons with ChatDev described on page 8?", 
    verbose=True
)
```

### Análise de Comportamento (Observabilidade)

Com `verbose=True`, o log de execução demonstra o raciocínio multietapa instanciado em uma única chamada:

1. Avalia as ferramentas disponíveis (`vector_query_tool` vs `summary_tool`).
    
2. Escolhe `vector_query_tool` (identifica que a query pede informação específica e aponta uma página).
    
3. Infere os parâmetros: `{'query': 'MetaGPT comparisons with ChatDev', 'page_numbers': ['8']}`.
    
4. Executa a função Python e retorna a resposta baseada no chunk filtrado.
    
5. A resposta mantém rastreabilidade de linhagem (lineage) através de `response.source_nodes[0].metadata`, permitindo assertividade programática em testes (ex: verificar se o nó retornado realmente tem `page_label == 8`).
    

---

### Tags & Referências

- #AgenticRAG #ToolCalling #FunctionCalling #AutoRetrieval #MetadataFiltering #LlamaIndex #LLMOps