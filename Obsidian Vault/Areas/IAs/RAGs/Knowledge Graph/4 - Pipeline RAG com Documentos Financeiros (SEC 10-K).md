
Nesta etapa, você aprenderá a transformar documentos estruturados (JSON extraídos de relatórios anuais) em uma base de conhecimento pesquisável, lidando com grandes volumes de texto através de técnicas de fragmentação (_chunking_) e indexação vetorial.

## 1. Preparação e Ingestão de Dados

Os relatórios 10-K são densos e contêm seções críticas como o "Item 1" (Visão Geral do Negócio). O processo inicia com o carregamento desses dados e a configuração do ambiente Neo4j e OpenAI.

```python
# Inicialização do Grafo e Constantes Globais
VECTOR_INDEX_NAME = 'form_10k_chunks'
VECTOR_NODE_LABEL = 'Chunk'
VECTOR_SOURCE_PROPERTY = 'text'
VECTOR_EMBEDDING_PROPERTY = 'textEmbedding'

kg = Neo4jGraph(
    url=NEO4J_URI, username=NEO4J_USERNAME, 
    password=NEO4J_PASSWORD, database=NEO4J_DATABASE
)
```

## 2. Estratégia de Chunking (Recursive Character Splitting)

Para que o LLM processe o contexto de forma eficiente, textos longos devem ser divididos em pedaços (_chunks_). Utilizamos o `RecursiveCharacterTextSplitter` do LangChain para manter a integridade semântica com sobreposição (_overlap_) de texto.

- **Chunk Size:** 2000 caracteres.
    
- **Chunk Overlap:** 200 caracteres (garante que o contexto não seja cortado abruptamente entre chunks).
    

## 3. Criação de Nós e Restrições no Grafo

Cada fragmento de texto torna-se um nó do tipo `:Chunk` no Neo4j, carregando metadados como o ID do formulário, o item de origem (ex: Item 1) e informações da empresa (CIK, nomes).

- **Constraint de Unicidade:** É fundamental garantir que cada `chunkId` seja único para evitar duplicidade durante re-ingestões.

```python
// Criando constraint de unicidade no Neo4j
CREATE CONSTRAINT unique_chunk IF NOT EXISTS 
FOR (c:Chunk) REQUIRE c.chunkId IS UNIQUE
```

## 4. Indexação Vetorial e Embeddings

Com os nós criados, geramos os vetores de embedding para a propriedade `text` e os armazenamos na propriedade `textEmbedding`.

- **Vector Index:** O índice permite buscas de similaridade de cosseno em alta velocidade.
    
- **OpenAI API:** O Neo4j chama o modelo de embedding da OpenAI diretamente para preencher o índice.
    

## 5. Implementação do RAG com LangChain

A integração final transforma o Neo4j em um `vector_store` para o LangChain, permitindo o uso de cadeias de perguntas e respostas (_RetrievalQA_).

```python
# Configuração do Retriever no LangChain
neo4j_vector_store = Neo4jVector.from_existing_graph(
    embedding=OpenAIEmbeddings(),
    index_name=VECTOR_INDEX_NAME,
    node_label=VECTOR_NODE_LABEL,
    text_node_properties=[VECTOR_SOURCE_PROPERTY],
    embedding_node_property=VECTOR_EMBEDDING_PROPERTY,
)
retriever = neo4j_vector_store.as_retriever()
```

## Mitigação de Alucinações via Prompt Engineering

Um risco comum em sistemas RAG é a **alucinação**: o modelo responder sobre temas fora do contexto (ex: responder sobre "Apple" usando dados da "NetApp").

- **A Solução:** Instruir explicitamente o modelo no prompt: _"Se você não tiver certeza da resposta, diga que não sabe"_. Isso garante que o sistema seja honesto sobre os limites da sua base de conhecimento.
## Implementação

```python
# Lesson 4: Constructing a Knowledge Graph from Text Documents[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Lesson-4:-Constructing-a-Knowledge-Graph-from-Text-Documents)

**Note:** This notebook takes about 30 seconds to be ready to use. Please wait until the "Kernel starting, please wait..." message clears from the top of the notebook before running any cells. You may start the video while you wait.

### Import packages and set up Neo4j[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Import-packages-and-set-up-Neo4j)

from dotenv import load_dotenv

import os

​

# Common data processing

import json

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

OPENAI_API_KEY = os.getenv('OPENAI_API_KEY')

# Note the code below is unique to this course environment, and not a 

# standard part of Neo4j's integration with OpenAI. Remove if running 

# in your own environment.

OPENAI_ENDPOINT = os.getenv('OPENAI_BASE_URL') + '/embeddings'

​

# Global constants

VECTOR_INDEX_NAME = 'form_10k_chunks'

VECTOR_NODE_LABEL = 'Chunk'

VECTOR_SOURCE_PROPERTY = 'text'

VECTOR_EMBEDDING_PROPERTY = 'textEmbedding'

### Take a look at a Form 10-K json file[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Take-a-look-at-a-Form-10-K-json-file)

- Publicly traded companies are required to fill a form 10-K each year with the Securities and Exchange Commision (SEC)
- You can search these filings using the SEC's [EDGAR database](https://www.sec.gov/edgar/search/)
- For the next few lessons, you'll work with a single 10-K form for a company called [NetApp](https://www.netapp.com/)

first_file_name = "./data/form10k/0000950170-23-027948.json"

​

first_file_as_object = json.load(open(first_file_name))

type(first_file_as_object)

for k,v in first_file_as_object.items():

    print(k, type(v))

item1_text = first_file_as_object['item1']

item1_text[0:1500]

### Split Form 10-K sections into chunks[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Split-Form-10-K-sections-into-chunks)

- Set up text splitter using LangChain
- For now, split only the text from the "item 1" section

text_splitter = RecursiveCharacterTextSplitter(

    chunk_size = 2000,

    chunk_overlap  = 200,

    length_function = len,

    is_separator_regex = False,

)

item1_text_chunks = text_splitter.split_text(item1_text)

type(item1_text_chunks)

len(item1_text_chunks)

item1_text_chunks[0]

- Set up helper function to chunk all sections of the Form 10-K
- You'll limit the number of chunks in each section to 20 to speed things up

def split_form10k_data_from_file(file):

    chunks_with_metadata = [] # use this to accumlate chunk records

    file_as_object = json.load(open(file)) # open the json file

    for item in ['item1','item1a','item7','item7a']: # pull these keys from the json

        print(f'Processing {item} from {file}') 

        item_text = file_as_object[item] # grab the text of the item

        item_text_chunks = text_splitter.split_text(item_text) # split the text into chunks

        chunk_seq_id = 0

        for chunk in item_text_chunks[:20]: # only take the first 20 chunks

            form_id = file[file.rindex('/') + 1:file.rindex('.')] # extract form id from file name

            # finally, construct a record with metadata and the chunk text

            chunks_with_metadata.append({

                'text': chunk, 

                # metadata from looping...

                'f10kItem': item,

                'chunkSeqId': chunk_seq_id,

                # constructed metadata...

                'formId': f'{form_id}', # pulled from the filename

                'chunkId': f'{form_id}-{item}-chunk{chunk_seq_id:04d}',

                # metadata from file...

                'names': file_as_object['names'],

                'cik': file_as_object['cik'],

                'cusip6': file_as_object['cusip6'],

                'source': file_as_object['source'],

            })

            chunk_seq_id += 1

        print(f'\tSplit into {chunk_seq_id} chunks')

    return chunks_with_metadata

first_file_chunks = split_form10k_data_from_file(first_file_name)

first_file_chunks[0]

### Create graph nodes using text chunks[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Create-graph-nodes-using-text-chunks)

merge_chunk_node_query = """

MERGE(mergedChunk:Chunk {chunkId: $chunkParam.chunkId})

    ON CREATE SET 

        mergedChunk.names = $chunkParam.names,

        mergedChunk.formId = $chunkParam.formId, 

        mergedChunk.cik = $chunkParam.cik, 

        mergedChunk.cusip6 = $chunkParam.cusip6, 

        mergedChunk.source = $chunkParam.source, 

        mergedChunk.f10kItem = $chunkParam.f10kItem, 

        mergedChunk.chunkSeqId = $chunkParam.chunkSeqId, 

        mergedChunk.text = $chunkParam.text

RETURN mergedChunk

"""

- Set up connection to graph instance using LangChain

kg = Neo4jGraph(

    url=NEO4J_URI, username=NEO4J_USERNAME, password=NEO4J_PASSWORD, database=NEO4J_DATABASE

)

- Create a single chunk node for now

kg.query(merge_chunk_node_query, 

         params={'chunkParam':first_file_chunks[0]})

- Create a uniqueness constraint to avoid duplicate chunks

kg.query("""

CREATE CONSTRAINT unique_chunk IF NOT EXISTS 

    FOR (c:Chunk) REQUIRE c.chunkId IS UNIQUE

""")

​

kg.query("SHOW INDEXES")

- Loop through and create nodes for all chunks
- Should create 23 nodes because you set a limit of 20 chunks in the text splitting function above

node_count = 0

for chunk in first_file_chunks:

    print(f"Creating `:Chunk` node for chunk ID {chunk['chunkId']}")

    kg.query(merge_chunk_node_query, 

            params={

                'chunkParam': chunk

            })

    node_count += 1

print(f"Created {node_count} nodes")

kg.query("""

         MATCH (n)

         RETURN count(n) as nodeCount

         """)

### Create a vector index[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Create-a-vector-index)

kg.query("""

         CREATE VECTOR INDEX `form_10k_chunks` IF NOT EXISTS

          FOR (c:Chunk) ON (c.textEmbedding) 

          OPTIONS { indexConfig: {

            `vector.dimensions`: 1536,

            `vector.similarity_function`: 'cosine'    

         }}

""")

kg.query("SHOW INDEXES")

### Calculate embedding vectors for chunks and populate index[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Calculate-embedding-vectors-for-chunks-and-populate-index)

- This query calculates the embedding vector and stores it as a property called `textEmbedding` on each `Chunk` node.

kg.query("""

    MATCH (chunk:Chunk) WHERE chunk.textEmbedding IS NULL

    WITH chunk, genai.vector.encode(

      chunk.text, 

      "OpenAI", 

      {

        token: $openAiApiKey, 

        endpoint: $openAiEndpoint

      }) AS vector

    CALL db.create.setNodeVectorProperty(chunk, "textEmbedding", vector)

    """, 

    params={"openAiApiKey":OPENAI_API_KEY, "openAiEndpoint": OPENAI_ENDPOINT} )

kg.refresh_schema()

print(kg.schema)

### Use similarity search to find relevant chunks[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Use-similarity-search-to-find-relevant-chunks)

- Setup a help function to perform similarity search using the vector index

def neo4j_vector_search(question):

  """Search for similar nodes using the Neo4j vector index"""

  vector_search_query = """

    WITH genai.vector.encode(

      $question, 

      "OpenAI", 

      {

        token: $openAiApiKey,

        endpoint: $openAiEndpoint

      }) AS question_embedding

    CALL db.index.vector.queryNodes($index_name, $top_k, question_embedding) yield node, score

    RETURN score, node.text AS text

  """

  similar = kg.query(vector_search_query, 

                     params={

                      'question': question, 

                      'openAiApiKey':OPENAI_API_KEY,

                      'openAiEndpoint': OPENAI_ENDPOINT,

                      'index_name':VECTOR_INDEX_NAME, 

                      'top_k': 10})

  return similar

- Ask a question!

search_results = neo4j_vector_search(

    'In a single sentence, tell me about Netapp.'

)

search_results[0]

### Set up a LangChain RAG workflow to chat with the form[](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Set-up-a-LangChain-RAG-workflow-to-chat-with-the-form)

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

​

retriever = neo4j_vector_store.as_retriever()

- Set up a RetrievalQAWithSourcesChain to carry out question answering
- You can check out the LangChain documentation for this chain [here](https://api.python.langchain.com/en/latest/chains/langchain.chains.qa_with_sources.retrieval.RetrievalQAWithSourcesChain.html)

chain = RetrievalQAWithSourcesChain.from_chain_type(

    ChatOpenAI(temperature=0), 

    chain_type="stuff", 

    retriever=retriever

)

def prettychain(question: str) -> str:

    """Pretty print the chain's response to a question"""

    response = chain({"question": question},

        return_only_outputs=True,)

    print(textwrap.fill(response['answer'], 60))

- Ask a question!

question = "What is Netapp's primary business?"

prettychain(question)

prettychain("Where is Netapp headquartered?")

prettychain("""

    Tell me about Netapp. 

    Limit your answer to a single sentence.

""")

prettychain("""

    Tell me about Apple. 

    Limit your answer to a single sentence.

""")

prettychain("""

    Tell me about Apple. 

    Limit your answer to a single sentence.

    If you are unsure about the answer, say you don't know.

""")

### Ask you own question![](https://s172-29-117-69p8888.lab-aws-production.deeplearning.ai/notebooks/23003/L4-construct_kg_from_text.ipynb#Ask-you-own-question!)

- Add your own question to the call to prettychain below to find out more about NetApp
- Here is NetApp's website if you want some inspiration: [https://www.netapp.com/](https://www.netapp.com/)

prettychain("""

    ADD YOUR OWN QUESTION HERE

""")
```