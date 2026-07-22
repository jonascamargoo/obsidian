---
tipo: aula
area: IAs
tags:
- ia/rag
- ia/knowledge-graph
criada: '2026-03-16'
---

O objetivo desta etapa é enriquecer as entidades de "Empresa" no grafo com informações sobre seus **gestores de investimento institucionais**. Isso transforma o grafo de um repositório de documentos em um mapa de dinâmica de mercado.

## 1. Ingestão e Estruturação de Dados de Terceiros

Os dados do Form 13 detalham quais firmas de investimento detêm ações de quais empresas públicas.

- **Processamento de CSV:** Os dados, originalmente XML, são processados via `csv.DictReader`, convertendo cada linha (investimento) em um dicionário Python.
    
- **Modelagem de Entidades:**
    
    - **`:Manager`:** Representa a firma de investimento. É identificada de forma única pelo seu CIK (Central Index Key).
        
    - **`:Company`:** Representa a empresa investida (ex: NetApp). É identificada pelo código **CUSIP 6**.
        

## 2. Enriquecimento de Nós e Full-Text Search

Diferente da busca vetorial (similaridade de conceitos), implementamos um **Índice de Texto Completo (Full-Text Index)** nos nós de gestores.

- **Vector vs. Full-Text:** Enquanto o vetor busca por "significado", o Full-Text busca por "grafia similar", o que é vital para encontrar nomes de empresas ou gestores específicos (ex: "Royal Bank of Canada").
    
- **Unificação:** O nó `:Company` criado agora é fundido com o nó `:Form` (do 10-K) através do identificador CUSIP 6, criando uma ponte entre o texto do relatório e os dados de posse de ações.

```python
// Criando o relacionamento de posse de ações com propriedades temporais
MATCH (m:Manager {managerCik: $cik}), (c:Company {cusip6: $cusip6})
MERGE (m)-[owns:OWN_STOCK_IN {reportCalendarOrQuarter: $quarter}]->(c)
ON CREATE SET owns.shares = $shares, owns.value = $value
```


## 3. Navegação Multicamadas (Multi-hop Patterns)

A verdadeira força desta arquitetura surge na capacidade de descrever padrões que cruzam diferentes domínios de dados em uma única query.

**O Padrão de Exploração:** `(:Chunk) -> (:Form) -> (:Company) <- [:OWN_STOCK_IN] - (:Manager)`

Este caminho permite que, ao encontrar um parágrafo relevante sobre tecnologia em um relatório (via busca vetorial), o sistema identifique instantaneamente **quem são os maiores investidores** da empresa que escreveu aquele parágrafo.

## 4. RAG com Contexto de Investimento (Investment Chain)

Integramos essa lógica ao LangChain através de uma **Retrieval Query** customizada que transforma os dados estruturados do grafo em sentenças legíveis para o LLM.

- **Tradução Grafo -> Texto:** A query Cypher recupera os 10 maiores investidores, calcula o valor monetário e concatena em frases: _"X firma detém Y ações avaliadas em Z"_.
    
- **Resultados:** * O **RAG Tradicional** (Plain Chain) descreve a empresa de forma genérica com base no texto.
    
    - O **GraphRAG Híbrido** (Investment Chain) fornece uma visão holística, listando os principais acionistas institucionais (ex: Vanguard, BlackRock) quando questionado sobre quem investe na empresa.
        

---

## ⚖️ Análise de Qualidade: Superando a Alucinação

Nos testes, o RAG tradicional alucinou ao descrever investidores como "uma base de clientes diversificada", pois não tinha acesso aos dados reais. O GraphRAG, ao injetar fatos extraídos diretamente das relações `OWN_STOCK_IN`, forçou o LLM a ser factualmente preciso.

> [!TIP] **Insight de Engenharia** A "arte" do GraphRAG reside em como você traduz os dados estruturados do grafo em linguagem natural antes de enviá-los ao LLM. Formatar valores monetários e nomes de firmas ajuda o modelo a "entender" o contexto injetado.


## Implementação

```python
# Lesson 6: Expanding the SEC Knowledge Graph[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Lesson-6:-Expanding-the-SEC-Knowledge-Graph)

**Note:** This notebook takes about 30 seconds to be ready to use. Please wait until the "Kernel starting, please wait..." message clears from the top of the notebook before running any cells. You may start the video while you wait.

### Import packages and set up Neo4j[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Import-packages-and-set-up-Neo4j)

from dotenv import load_dotenv

import os

import textwrap

​

# Langchain

from langchain_community.graphs import Neo4jGraph

from langchain_community.vectorstores import Neo4jVector

from langchain_openai import OpenAIEmbeddings

from langchain.text_splitter import RecursiveCharacterTextSplitter

from langchain.chains import RetrievalQAWithSourcesChain

from langchain_openai import ChatOpenAI

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

kg = Neo4jGraph(

    url=NEO4J_URI, 

    username=NEO4J_USERNAME, 

    password=NEO4J_PASSWORD, 

    database=NEO4J_DATABASE

)

### Read the collection of Form 13s[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Read-the-collection-of-Form-13s)

- Investment management firms must report on their investments in companies to the SEC by filing a document called **Form 13**
- You'll load a collection of Form 13 for managers that have invested in NetApp
- You can check out the CSV file by navigating to the data directory using the File menu at the top of the notebook

import csv

​

all_form13s = []

​

with open('./data/form13.csv', mode='r') as csv_file:

    csv_reader = csv.DictReader(csv_file)

    for row in csv_reader: # each row will be a dictionary

      all_form13s.append(row)

- Look at the contents of the first 5 Form 13s

all_form13s[0:5]

len(all_form13s)

### Create company nodes in the graph[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Create-company-nodes-in-the-graph)

- Use the companies identified in the Form 13s to create `Company` nodes
- For now, there is only one company - NetApp

# work with just the first form fow now

first_form13 = all_form13s[0]

​

cypher = """

MERGE (com:Company {cusip6: $cusip6})

  ON CREATE

    SET com.companyName = $companyName,

        com.cusip = $cusip

"""

​

kg.query(cypher, params={

    'cusip6':first_form13['cusip6'], 

    'companyName':first_form13['companyName'], 

    'cusip':first_form13['cusip'] 

})

cypher = """

MATCH (com:Company)

RETURN com LIMIT 1

"""

​

kg.query(cypher)

- Update the company name to match Form 10-K

cypher = """

  MATCH (com:Company), (form:Form)

    WHERE com.cusip6 = form.cusip6

  RETURN com.companyName, form.names

"""

​

kg.query(cypher)

cypher = """

  MATCH (com:Company), (form:Form)

    WHERE com.cusip6 = form.cusip6

  SET com.names = form.names

"""

​

kg.query(cypher)

- Create a `FILED` relationship between the company and the Form-10K node

kg.query("""

  MATCH (com:Company), (form:Form)

    WHERE com.cusip6 = form.cusip6

  MERGE (com)-[:FILED]->(form)

""")

​

### Create manager nodes[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Create-manager-nodes)

- Create a `manager` node for companies that have filed a Form 13 to report their investment in NetApp
- Start with the single manager who filed the first Form 13 in the list

cypher = """

  MERGE (mgr:Manager {managerCik: $managerParam.managerCik})

    ON CREATE

        SET mgr.managerName = $managerParam.managerName,

            mgr.managerAddress = $managerParam.managerAddress

"""

​

kg.query(cypher, params={'managerParam': first_form13})

kg.query("""

  MATCH (mgr:Manager)

  RETURN mgr LIMIT 1

""")

- Create a uniquness constraint to avoid duplicate managers

kg.query("""

CREATE CONSTRAINT unique_manager 

  IF NOT EXISTS

  FOR (n:Manager) 

  REQUIRE n.managerCik IS UNIQUE

""")

- Create a fulltext index of manager names to enable text search

kg.query("""

CREATE FULLTEXT INDEX fullTextManagerNames

  IF NOT EXISTS

  FOR (mgr:Manager) 

  ON EACH [mgr.managerName]

""")

​

kg.query("""

  CALL db.index.fulltext.queryNodes("fullTextManagerNames", 

      "royal bank") YIELD node, score

  RETURN node.managerName, score

""")

- Create nodes for all companies that filed a Form 13

cypher = """

  MERGE (mgr:Manager {managerCik: $managerParam.managerCik})

    ON CREATE

        SET mgr.managerName = $managerParam.managerName,

            mgr.managerAddress = $managerParam.managerAddress

"""

# loop through all Form 13s

for form13 in all_form13s:

  kg.query(cypher, params={'managerParam': form13 })

kg.query("""

    MATCH (mgr:Manager) 

    RETURN count(mgr)

""")

### Create relationships between managers and companies[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Create-relationships-between-managers-and-companies)

- Match companies with managers based on data in the Form 13
- Create an `OWNS_STOCK_IN` relationship between the manager and the company
- Start with the single manager who filed the first Form 13 in the list

cypher = """

  MATCH (mgr:Manager {managerCik: $investmentParam.managerCik}), 

        (com:Company {cusip6: $investmentParam.cusip6})

  RETURN mgr.managerName, com.companyName, $investmentParam as investment

"""

​

kg.query(cypher, params={ 

    'investmentParam': first_form13 

})

cypher = """

MATCH (mgr:Manager {managerCik: $ownsParam.managerCik}), 

        (com:Company {cusip6: $ownsParam.cusip6})

MERGE (mgr)-[owns:OWNS_STOCK_IN { 

    reportCalendarOrQuarter: $ownsParam.reportCalendarOrQuarter

}]->(com)

ON CREATE

    SET owns.value  = toFloat($ownsParam.value), 

        owns.shares = toInteger($ownsParam.shares)

RETURN mgr.managerName, owns.reportCalendarOrQuarter, com.companyName

"""

​

kg.query(cypher, params={ 'ownsParam': first_form13 })

kg.query("""

MATCH (mgr:Manager {managerCik: $ownsParam.managerCik})

-[owns:OWNS_STOCK_IN]->

        (com:Company {cusip6: $ownsParam.cusip6})

RETURN owns { .shares, .value }

""", params={ 'ownsParam': first_form13 })

- Create relationships between all of the managers who filed Form 13s and the company

cypher = """

MATCH (mgr:Manager {managerCik: $ownsParam.managerCik}), 

        (com:Company {cusip6: $ownsParam.cusip6})

MERGE (mgr)-[owns:OWNS_STOCK_IN { 

    reportCalendarOrQuarter: $ownsParam.reportCalendarOrQuarter 

    }]->(com)

  ON CREATE

    SET owns.value  = toFloat($ownsParam.value), 

        owns.shares = toInteger($ownsParam.shares)

"""

​

#loop through all Form 13s

for form13 in all_form13s:

  kg.query(cypher, params={'ownsParam': form13 })

cypher = """

  MATCH (:Manager)-[owns:OWNS_STOCK_IN]->(:Company)

  RETURN count(owns) as investments

"""

​

kg.query(cypher)

kg.refresh_schema()

print(textwrap.fill(kg.schema, 60))

### Determine the number of investors[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Determine-the-number-of-investors)

- Start by finding a form 10-K chunk, and save to use in subsequent queries

cypher = """

    MATCH (chunk:Chunk)

    RETURN chunk.chunkId as chunkId LIMIT 1

    """

​

chunk_rows = kg.query(cypher)

print(chunk_rows)

chunk_first_row = chunk_rows[0]

print(chunk_first_row)

ref_chunk_id = chunk_first_row['chunkId']

ref_chunk_id

- Build up path from Form 10-K chunk to companies and managers

cypher = """

    MATCH (:Chunk {chunkId: $chunkIdParam})-[:PART_OF]->(f:Form)

    RETURN f.source

    """

​

kg.query(cypher, params={'chunkIdParam': ref_chunk_id})

cypher = """

MATCH (:Chunk {chunkId: $chunkIdParam})-[:PART_OF]->(f:Form),

    (com:Company)-[:FILED]->(f)

RETURN com.companyName as name

"""

​

kg.query(cypher, params={'chunkIdParam': ref_chunk_id})

cypher = """

MATCH (:Chunk {chunkId: $chunkIdParam})-[:PART_OF]->(f:Form),

        (com:Company)-[:FILED]->(f),

        (mgr:Manager)-[:OWNS_STOCK_IN]->(com)

RETURN com.companyName, 

        count(mgr.managerName) as numberOfinvestors 

LIMIT 1

"""

​

kg.query(cypher, params={

    'chunkIdParam': ref_chunk_id

})

### Use queries to build additional context for LLM[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Use-queries-to-build-additional-context-for-LLM)

- Create sentences that indicate how much stock a manager has invested in a company

cypher = """

    MATCH (:Chunk {chunkId: $chunkIdParam})-[:PART_OF]->(f:Form),

        (com:Company)-[:FILED]->(f),

        (mgr:Manager)-[owns:OWNS_STOCK_IN]->(com)

    RETURN mgr.managerName + " owns " + owns.shares + 

        " shares of " + com.companyName + 

        " at a value of $" + 

        apoc.number.format(toInteger(owns.value)) AS text

    LIMIT 10

    """

kg.query(cypher, params={

    'chunkIdParam': ref_chunk_id

})

results = kg.query(cypher, params={

    'chunkIdParam': ref_chunk_id

})

print(textwrap.fill(results[0]['text'], 60))

- Create a plain Question Answer chain
- Similarity search only, no augmentation by Cypher Query

vector_store = Neo4jVector.from_existing_graph(

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

retriever = vector_store.as_retriever()

​

# Create a chatbot Question & Answer chain from the retriever

plain_chain = RetrievalQAWithSourcesChain.from_chain_type(

    ChatOpenAI(temperature=0), 

    chain_type="stuff", 

    retriever=retriever

)

- Create a second QA chain
- Augment similarity search using sentences found by the investment query above

investment_retrieval_query = """

MATCH (node)-[:PART_OF]->(f:Form),

    (f)<-[:FILED]-(com:Company),

    (com)<-[owns:OWNS_STOCK_IN]-(mgr:Manager)

WITH node, score, mgr, owns, com 

    ORDER BY owns.shares DESC LIMIT 10

WITH collect (

    mgr.managerName + 

    " owns " + owns.shares + 

    " shares in " + com.companyName + 

    " at a value of $" + 

    apoc.number.format(toInteger(owns.value)) + "." 

) AS investment_statements, node, score

RETURN apoc.text.join(investment_statements, "\n") + 

    "\n" + node.text AS text,

    score,

    { 

      source: node.source

    } as metadata

"""

vector_store_with_investment = Neo4jVector.from_existing_index(

    OpenAIEmbeddings(),

    url=NEO4J_URI,

    username=NEO4J_USERNAME,

    password=NEO4J_PASSWORD,

    database="neo4j",

    index_name=VECTOR_INDEX_NAME,

    text_node_property=VECTOR_SOURCE_PROPERTY,

    retrieval_query=investment_retrieval_query,

)

​

# Create a retriever from the vector store

retriever_with_investments = vector_store_with_investment.as_retriever()

​

# Create a chatbot Question & Answer chain from the retriever

investment_chain = RetrievalQAWithSourcesChain.from_chain_type(

    ChatOpenAI(temperature=0), 

    chain_type="stuff", 

    retriever=retriever_with_investments

)

- Compare the outputs!

question = "In a single sentence, tell me about Netapp."

plain_chain(

    {"question": question},

    return_only_outputs=True,

)

investment_chain(

    {"question": question},

    return_only_outputs=True,

)

- The LLM didn't make use of the investor information since the question didn't ask about investors
- Change the question and ask again

question = "In a single sentence, tell me about Netapp investors."

plain_chain(

    {"question": question},

    return_only_outputs=True,

)

investment_chain(

    {"question": question},

    return_only_outputs=True,

)

### Try for yourself[](https://s172-29-23-178p8888.lab-aws-production.deeplearning.ai/notebooks/23005/L6-expand_the_kg.ipynb#Try-for-yourself)

- Try changing the query above to retrieve other information
- Try asking different questions
- Note, if you change the Cypher query, you'll need to reset the retriever and QA chain

```