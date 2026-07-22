---
tipo: aula
area: IAs
tags:
- ia/rag
- ia/knowledge-graph
criada: '2026-03-16'
---

Nesta aula, o objetivo é replicar a estrutura lógica de um documento financeiro (Form 10-K) dentro do grafo, conectando os fragmentos (_chunks_) de texto para refletir a hierarquia original do relatório.

## 1. Modelagem da Entidade de Topo (`:Form`)

Antes de conectar os chunks, criamos um nó central para representar o formulário 10-K. Este nó armazena metadados globais como o CIK (Central Index Key) e o link da SEC
![[Pasted image 20260315232418.png]]

No estágio inicial da aula anterior, tínhamos apenas nós `:Chunk` isolados que continham, cada um, cópias redundantes dos metadados da empresa (como CIK e Nome).

A criação do nó `:Form` serve para:

1. **Reduzir Redundância:** Movemos metadados globais para um único ponto de referência.
    
2. **Ponto de Entrada (Entry Point):** Ele funciona como a "raiz" de uma árvore documental. Em vez de pesquisar em milhões de chunks, você pode filtrar pelo formulário específico e navegar para seus filhos.
    
3. **Segurança e Governança:** Se você precisar atualizar o link da SEC (`source`), você altera em um único nó, em vez de milhares de chunks.
### Os Atributos Técnicos do Nó

O nó é definido com as seguintes propriedades estruturais:

- **`formId`:** O identificador único (Primary Key) que vincula logicamente todos os fragmentos ao documento original.
    
- **`cik` (Central Index Key):** O identificador numérico oficial da SEC para a empresa. Para um engenheiro de dados, este é o ID de integração com fontes externas.
    
- **`source`:** A URL absoluta para o documento bruto (.xml ou .html) no banco de dados EDGAR da SEC.
    
- **`names`:** O nome (ou lista de nomes/razões sociais) da entidade que submeteu o relatório.
    
### O Processo de Criação (Engenharia de Query)

Diferente de um `INSERT` tradicional, o autor utiliza uma técnica comum em pipelines de dados: **Projeção e Migração**.

1. **Extração de Amostra:** Como os chunks já possuem os metadados embutidos de quando foram criados, a query busca **um único chunk** e "projeta" (extrai) seus metadados para um dicionário Python.
    
2. **MERGE Parametrizado:** O comando `MERGE` é utilizado para garantir **idempotência**. Se o pipeline rodar novamente para o mesmo `formId`, o sistema não criará duplicatas, apenas garantirá que as propriedades estejam corretas.
    

### Visão do Arquiteto

Ao isolar o formulário como uma entidade de topo, você habilita buscas complexas que seriam impossíveis no RAG tradicional. Por exemplo:

> _"Recupere todos os chunks que falam sobre riscos financeiros, mas apenas para formulários submetidos pelo CIK X no ano de 2024."_

No Grafo, isso é um salto simples entre o nó `:Form` e os nós `:Chunk`. No RAG tradicional, isso exigiria um filtro de metadados pesado sobre todo o índice vetorial.
---

```python
# Recuperando metadados de um chunk existente para criar o nó Form
form_info_query = "MATCH (c:Chunk) RETURN c {.cik, .source, .formId, .names} LIMIT 1"
form_info = kg.query(form_info_query)[0]

# Criando o nó :Form de maneira parametrizada
create_form_query = """
MERGE (f:Form {formId: $formInfo.formId})
SET f.names = $formInfo.names, f.cik = $formInfo.cik, f.source = $formInfo.source
"""
kg.query(create_form_query, params={'formInfo': form_info})
```

## 2. Criando a Estrutura: Listas Ligadas e Hierarquia

A inovação técnica aqui é transformar dados sequenciais em uma **Lista Ligada** de nós dentro do grafo.

![[Pasted image 20260315232849.png]]

### A. Relacionamento `NEXT`

Conectamos os chunks de uma mesma seção em ordem sequencial. Isso permite que, ao encontrar um chunk via busca vetorial, o sistema "olhe" para os parágrafos anteriores e posteriores de forma exata.

```python
// Criando o relacionamento NEXT entre chunks sequenciais
MATCH (c:Chunk {formId: $formId, f10kItem: $item})
WITH c ORDER BY c.chunkSeqId
WITH collect(c) AS section_chunks
UNWIND range(0, size(section_chunks)-2) AS i
WITH section_chunks[i] AS c1, section_chunks[i+1] AS c2
MERGE (c1)-[:NEXT]->(c2) //
```

### B. Relacionamentos `PART_OF` e `SECTION`

- **`PART_OF`:** Conecta cada chunk ao seu formulário pai.
    
- **`SECTION`:** Uma "ponte" rápida que conecta o nó `:Form` diretamente ao primeiro chunk (sequência 0) de cada seção.
    

---

## 3. Navegação e Caminhos (Paths)

Com a estrutura pronta, introduzimos o conceito de **Path** (Caminho). Um caminho é uma sequência de nós e relacionamentos capturada como uma variável.

### Janela de Contexto Dinâmica (Chunk Window)

Em vez de enviar apenas o chunk encontrado pela busca vetorial ao LLM, podemos capturar uma "janela" de contexto (o chunk atual + os adjacentes).

```python
// Recuperando uma janela de 3 chunks (anterior, atual, próximo)
MATCH (c1)-[:NEXT]->(c2)-[:NEXT]->(c3)
WHERE c2.chunkId = $targetChunkId
RETURN c1.text + c2.text + c3.text AS expandedContext //
```

## Análise Comparativa: RAG Tradicional vs. GraphRAG

|**Recurso**|**RAG Vetorial (Windowless)**|**GraphRAG (Com Chunk Window)**|
|---|---|---|
|**Recuperação**|Baseada apenas em similaridade estatística.|Similaridade + Estrutura Determinística.|
|**Contexto**|Fragmentado (pode cortar frases).|Coeso (recupera a sequência lógica).|
|**Resultado**|Respostas diretas, mas às vezes incompletas.|Respostas mais ricas e detalhadas (ex: cita produtos específicos como "NetApp Keystone").|

### 🚀 O Poder da "Retrieval Query" no LangChain

A integração do Neo4j com LangChain permite passar uma **Retrieval Query** personalizada. Isso significa que o banco de dados realiza a busca vetorial e, _antes de retornar ao LLM_, executa uma lógica Cypher para expandir o contexto, reduzindo a carga de processamento na aplicação.

## Implementação

```python
# Lesson 5: Adding Relationships to the SEC Knowledge Graph[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Lesson-5:-Adding-Relationships-to-the-SEC-Knowledge-Graph)

**Note:** This notebook takes about 30 seconds to be ready to use. Please wait until the "Kernel starting, please wait..." message clears from the top of the notebook before running any cells. You may start the video while you wait.

### Import packages and set up Neo4j[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Import-packages-and-set-up-Neo4j)

from dotenv import load_dotenv

import os

​

# Common data processing

import textwrap

​

# Langchain

from langchain_community.graphs import Neo4jGraph

from langchain_community.vectorstores import Neo4jVector

from langchain.text_splitter import RecursiveCharacterTextSplitter

from langchain.chains import RetrievalQAWithSourcesChain

from langchain_openai import ChatOpenAI

from langchain_openai import OpenAIEmbeddings

​

# Warning control

import warnings

warnings.filterwarnings("ignore")

# Load from environment

load_dotenv('.env', override=True)

NEO4J_URI = os.getenv('NEO4J_URI')

NEO4J_USERNAME = os.getenv('NEO4J_USERNAME')

NEO4J_PASSWORD = os.getenv('NEO4J_PASSWORD')

NEO4J_DATABASE = os.getenv('NEO4J_DATABASE') or 'neo4j'

​

# Global constants

VECTOR_INDEX_NAME = 'form_10k_chunks'

VECTOR_NODE_LABEL = 'Chunk'

VECTOR_SOURCE_PROPERTY = 'text'

VECTOR_EMBEDDING_PROPERTY = 'textEmbedding'

​

kg = Neo4jGraph(

    url=NEO4J_URI, username=NEO4J_USERNAME, password=NEO4J_PASSWORD, database=NEO4J_DATABASE

)

### Create a Form 10-K node[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Create-a-Form-10-K-node)

- Create a node to represent the entire Form 10-K
- Populate with metadata taken from a single chunk of the form

cypher = """

  MATCH (anyChunk:Chunk) 

  WITH anyChunk LIMIT 1

  RETURN anyChunk { .names, .source, .formId, .cik, .cusip6 } as formInfo

"""

form_info_list = kg.query(cypher)

​

form_info_list

​

form_info = form_info_list[0]['formInfo']

form_info

cypher = """

    MERGE (f:Form {formId: $formInfoParam.formId })

      ON CREATE 

        SET f.names = $formInfoParam.names

        SET f.source = $formInfoParam.source

        SET f.cik = $formInfoParam.cik

        SET f.cusip6 = $formInfoParam.cusip6

"""

​

kg.query(cypher, params={'formInfoParam': form_info})

kg.query("MATCH (f:Form) RETURN count(f) as formCount")

### Create a linked list of Chunk nodes for each section[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Create-a-linked-list-of-Chunk-nodes-for-each-section)

- Start by identifying chunks from the same section

cypher = """

  MATCH (from_same_form:Chunk)

    WHERE from_same_form.formId = $formIdParam

  RETURN from_same_form {.formId, .f10kItem, .chunkId, .chunkSeqId } as chunkInfo

    LIMIT 10

"""

​

kg.query(cypher, params={'formIdParam': form_info['formId']})

- Order chunks by their sequence ID

cypher = """

  MATCH (from_same_form:Chunk)

    WHERE from_same_form.formId = $formIdParam

  RETURN from_same_form {.formId, .f10kItem, .chunkId, .chunkSeqId } as chunkInfo 

    ORDER BY from_same_form.chunkSeqId ASC

    LIMIT 10

"""

​

kg.query(cypher, params={'formIdParam': form_info['formId']})

- Limit chunks to just the "Item 1" section, the organize in ascending order

cypher = """

  MATCH (from_same_section:Chunk)

  WHERE from_same_section.formId = $formIdParam

    AND from_same_section.f10kItem = $f10kItemParam // NEW!!!

  RETURN from_same_section { .formId, .f10kItem, .chunkId, .chunkSeqId } 

    ORDER BY from_same_section.chunkSeqId ASC

    LIMIT 10

"""

​

kg.query(cypher, params={'formIdParam': form_info['formId'], 

                         'f10kItemParam': 'item1'})

​

- Collect ordered chunks into a list

cypher = """

  MATCH (from_same_section:Chunk)

  WHERE from_same_section.formId = $formIdParam

    AND from_same_section.f10kItem = $f10kItemParam

  WITH from_same_section { .formId, .f10kItem, .chunkId, .chunkSeqId } 

    ORDER BY from_same_section.chunkSeqId ASC

    LIMIT 10

  RETURN collect(from_same_section) // NEW!!!

"""

​

kg.query(cypher, params={'formIdParam': form_info['formId'], 

                         'f10kItemParam': 'item1'})

​

### Add a NEXT relationship between subsequent chunks[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Add-a-NEXT-relationship-between-subsequent-chunks)

- Use the `apoc.nodes.link` function from Neo4j to link ordered list of `Chunk` nodes with a `NEXT` relationship
- Do this for just the "Item 1" section to start

cypher = """

  MATCH (from_same_section:Chunk)

  WHERE from_same_section.formId = $formIdParam

    AND from_same_section.f10kItem = $f10kItemParam

  WITH from_same_section

    ORDER BY from_same_section.chunkSeqId ASC

  WITH collect(from_same_section) as section_chunk_list

    CALL apoc.nodes.link(

        section_chunk_list, 

        "NEXT", 

        {avoidDuplicates: true}

    )  // NEW!!!

  RETURN size(section_chunk_list)

"""

​

kg.query(cypher, params={'formIdParam': form_info['formId'], 

                         'f10kItemParam': 'item1'})

​

kg.refresh_schema()

print(kg.schema)

- Loop through and create relationships for all sections of the form 10-K

cypher = """

  MATCH (from_same_section:Chunk)

  WHERE from_same_section.formId = $formIdParam

    AND from_same_section.f10kItem = $f10kItemParam

  WITH from_same_section

    ORDER BY from_same_section.chunkSeqId ASC

  WITH collect(from_same_section) as section_chunk_list

    CALL apoc.nodes.link(

        section_chunk_list, 

        "NEXT", 

        {avoidDuplicates: true}

    )

  RETURN size(section_chunk_list)

"""

for form10kItemName in ['item1', 'item1a', 'item7', 'item7a']:

  kg.query(cypher, params={'formIdParam':form_info['formId'], 

                           'f10kItemParam': form10kItemName})

​

### Connect chunks to their parent form with a PART_OF relationship[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Connect-chunks-to-their-parent-form-with-a-PART_OF-relationship)

cypher = """

  MATCH (c:Chunk), (f:Form)

    WHERE c.formId = f.formId

  MERGE (c)-[newRelationship:PART_OF]->(f)

  RETURN count(newRelationship)

"""

​

kg.query(cypher)

### Create a SECTION relationship on first chunk of each section[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Create-a-SECTION-relationship-on-first-chunk-of-each-section)

cypher = """

  MATCH (first:Chunk), (f:Form)

  WHERE first.formId = f.formId

    AND first.chunkSeqId = 0

  WITH first, f

    MERGE (f)-[r:SECTION {f10kItem: first.f10kItem}]->(first)

  RETURN count(r)

"""

​

kg.query(cypher)

### Example cypher queries[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Example-cypher-queries)

- Return the first chunk of the Item 1 section

cypher = """

  MATCH (f:Form)-[r:SECTION]->(first:Chunk)

    WHERE f.formId = $formIdParam

        AND r.f10kItem = $f10kItemParam

  RETURN first.chunkId as chunkId, first.text as text

"""

​

first_chunk_info = kg.query(cypher, params={

    'formIdParam': form_info['formId'], 

    'f10kItemParam': 'item1'

})[0]

​

first_chunk_info

​

- Get the second chunk of the Item 1 section

cypher = """

  MATCH (first:Chunk)-[:NEXT]->(nextChunk:Chunk)

    WHERE first.chunkId = $chunkIdParam

  RETURN nextChunk.chunkId as chunkId, nextChunk.text as text

"""

​

next_chunk_info = kg.query(cypher, params={

    'chunkIdParam': first_chunk_info['chunkId']

})[0]

​

next_chunk_info

​

print(first_chunk_info['chunkId'], next_chunk_info['chunkId'])

- Return a window of three chunks

cypher = """

    MATCH (c1:Chunk)-[:NEXT]->(c2:Chunk)-[:NEXT]->(c3:Chunk) 

        WHERE c2.chunkId = $chunkIdParam

    RETURN c1.chunkId, c2.chunkId, c3.chunkId

    """

​

kg.query(cypher,

         params={'chunkIdParam': next_chunk_info['chunkId']})

### Information is stored in the structure of a graph[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Information-is-stored-in-the-structure-of-a-graph)

- Matched patterns of nodes and relationships in a graph are called **paths**
- The length of a path is equal to the number of relationships in the path
- Paths can be captured as variables and used elsewhere in queries

cypher = """

    MATCH window = (c1:Chunk)-[:NEXT]->(c2:Chunk)-[:NEXT]->(c3:Chunk) 

        WHERE c1.chunkId = $chunkIdParam

    RETURN length(window) as windowPathLength

    """

​

kg.query(cypher,

         params={'chunkIdParam': next_chunk_info['chunkId']})

### Finding variable length windows[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Finding-variable-length-windows)

- A pattern match will fail if the relationship doesn't exist in the graph
- For example, the first chunk in a section has no preceding chunk, so the next query won't return anything

cypher = """

    MATCH window=(c1:Chunk)-[:NEXT]->(c2:Chunk)-[:NEXT]->(c3:Chunk) 

        WHERE c2.chunkId = $chunkIdParam

    RETURN nodes(window) as chunkList

    """

# pull the chunk ID from the first 

kg.query(cypher,

         params={'chunkIdParam': first_chunk_info['chunkId']})

​

- Modify `NEXT` relationship to have variable length

cypher = """

  MATCH window=

      (:Chunk)-[:NEXT*0..1]->(c:Chunk)-[:NEXT*0..1]->(:Chunk) 

    WHERE c.chunkId = $chunkIdParam

  RETURN length(window)

  """

​

kg.query(cypher,

         params={'chunkIdParam': first_chunk_info['chunkId']})

- Retrieve only the longest path

cypher = """

  MATCH window=

      (:Chunk)-[:NEXT*0..1]->(c:Chunk)-[:NEXT*0..1]->(:Chunk)

    WHERE c.chunkId = $chunkIdParam

  WITH window as longestChunkWindow 

      ORDER BY length(window) DESC LIMIT 1

  RETURN length(longestChunkWindow)

  """

​

kg.query(cypher,

         params={'chunkIdParam': first_chunk_info['chunkId']})

### Customize the results of the similarity search using Cypher[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Customize-the-results-of-the-similarity-search-using-Cypher)

- Extend the vector store definition to accept a Cypher query
- The Cypher query takes the results of the vector similarity search and then modifies them in some way
- Start with a simple query that just returns some extra text along with the search results

retrieval_query_extra_text = """

WITH node, score, "Andreas knows Cypher. " as extraText

RETURN extraText + "\n" + node.text as text,

    score,

    node {.source} AS metadata

"""

- Set up the vector store to use the query, then instantiate a retriever and Question-Answer chain in LangChain

vector_store_extra_text = Neo4jVector.from_existing_index(

    embedding=OpenAIEmbeddings(),

    url=NEO4J_URI,

    username=NEO4J_USERNAME,

    password=NEO4J_PASSWORD,

    database="neo4j",

    index_name=VECTOR_INDEX_NAME,

    text_node_property=VECTOR_SOURCE_PROPERTY,

    retrieval_query=retrieval_query_extra_text, # NEW !!!

)

​

# Create a retriever from the vector store

retriever_extra_text = vector_store_extra_text.as_retriever()

​

# Create a chatbot Question & Answer chain from the retriever

chain_extra_text = RetrievalQAWithSourcesChain.from_chain_type(

    ChatOpenAI(temperature=0), 

    chain_type="stuff", 

    retriever=retriever_extra_text

)

- Ask a question!

chain_extra_text(

    {"question": "What topics does Andreas know about?"},

    return_only_outputs=True)

- Note, the LLM hallucinates here, using the information in the retrieved text as well as the extra text.
- Modify the prompt to try and get a more accurate answer

chain_extra_text(

    {"question": "What single topic does Andreas know about?"},

    return_only_outputs=True)

### Try for yourself![](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Try-for-yourself!)

- Modify the query below to add your own additional text
- Try engineering the prompt to refine your results
- Note, you'll need to reset the vector store, retriever, and chain each time you change the Cypher query.

# modify the retrieval extra text here then run the entire cell

retrieval_query_extra_text = """

WITH node, score, "Andreas knows Cypher. " as extraText

RETURN extraText + "\n" + node.text as text,

    score,

    node {.source} AS metadata

"""

​

vector_store_extra_text = Neo4jVector.from_existing_index(

    embedding=OpenAIEmbeddings(),

    url=NEO4J_URI,

    username=NEO4J_USERNAME,

    password=NEO4J_PASSWORD,

    database="neo4j",

    index_name=VECTOR_INDEX_NAME,

    text_node_property=VECTOR_SOURCE_PROPERTY,

    retrieval_query=retrieval_query_extra_text, # NEW !!!

)

​

# Create a retriever from the vector store

retriever_extra_text = vector_store_extra_text.as_retriever()

​

# Create a chatbot Question & Answer chain from the retriever

chain_extra_text = RetrievalQAWithSourcesChain.from_chain_type(

    ChatOpenAI(temperature=0), 

    chain_type="stuff", 

    retriever=retriever_extra_text

)

### Expand context around a chunk using a window[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Expand-context-around-a-chunk-using-a-window)

- First, create a regular vector store that retrieves a single node

neo4j_vector_store = Neo4jVector.from_existing_graph(

    embedding=OpenAIEmbeddings(),

    url=NEO4J_URI,

    username=NEO4J_USERNAME,

    password=NEO4J_PASSWORD,

    index_name=VECTOR_INDEX_NAME,

    node_label=VECTOR_NODE_LABEL,

    text_node_properties=[VECTOR_SOURCE_PROPERTY],

    embedding_node_property=VECTOR_EMBEDDING_PROPERTY,

)

# Create a retriever from the vector store

windowless_retriever = neo4j_vector_store.as_retriever()

​

# Create a chatbot Question & Answer chain from the retriever

windowless_chain = RetrievalQAWithSourcesChain.from_chain_type(

    ChatOpenAI(temperature=0), 

    chain_type="stuff", 

    retriever=windowless_retriever

)

- Next, define a window retrieval query to get consecutive chunks

retrieval_query_window = """

MATCH window=

    (:Chunk)-[:NEXT*0..1]->(node)-[:NEXT*0..1]->(:Chunk)

WITH node, score, window as longestWindow 

  ORDER BY length(window) DESC LIMIT 1

WITH nodes(longestWindow) as chunkList, node, score

  UNWIND chunkList as chunkRows

WITH collect(chunkRows.text) as textList, node, score

RETURN apoc.text.join(textList, " \n ") as text,

    score,

    node {.source} AS metadata

"""

​

- Set up a QA chain that will use the window retrieval query

vector_store_window = Neo4jVector.from_existing_index(

    embedding=OpenAIEmbeddings(),

    url=NEO4J_URI,

    username=NEO4J_USERNAME,

    password=NEO4J_PASSWORD,

    database="neo4j",

    index_name=VECTOR_INDEX_NAME,

    text_node_property=VECTOR_SOURCE_PROPERTY,

    retrieval_query=retrieval_query_window, # NEW!!!

)

​

# Create a retriever from the vector store

retriever_window = vector_store_window.as_retriever()

​

# Create a chatbot Question & Answer chain from the retriever

chain_window = RetrievalQAWithSourcesChain.from_chain_type(

    ChatOpenAI(temperature=0), 

    chain_type="stuff", 

    retriever=retriever_window

)

### Compare the two chains[](https://s172-29-108-209p8888.lab-aws-production.deeplearning.ai/notebooks/23004/L5-add_relationships_to_kg.ipynb#Compare-the-two-chains)

question = "In a single sentence, tell me about Netapp's business."

answer = windowless_chain(

    {"question": question},

    return_only_outputs=True,

)

print(textwrap.fill(answer["answer"]))

answer = chain_window(

    {"question": question},

    return_only_outputs=True,

)

print(textwrap.fill(answer["answer"]))
```