---
tipo: aula
area: IAs
tags:
- ia/rag
- ia/knowledge-graph
criada: '2026-03-16'
---

Para que um LLM encontre informações em um grafo de forma tão fluida quanto em documentos de texto, é necessário criar **índices vetoriais** sobre as propriedades de texto dos nós.

## 1. Setup de Infraestrutura e Embeddings

Além dos pacotes clássicos do Neo4j e LangChain, introduzimos o provedor de embeddings (neste caso, OpenAI).

```python
# Adicionando a chave de API necessária para o modelo de embedding
OPENAI_API_KEY = os.getenv('OPENAI_API_KEY') #

# A conexão via Neo4jGraph permite o envio de queries Cypher que 
# chamam funções de IA diretamente no banco.
kg = Neo4jGraph(
    url=NEO4J_URI, username=NEO4J_USERNAME, 
    password=NEO4J_PASSWORD, database=NEO4J_DATABASE
)
```

## 2. Criação do Índice Vetorial (Schema)

O primeiro passo no banco de dados não é a busca, mas a definição de onde os vetores "viverão".

- **Configuração do Índice:** Definimos o nome do índice, o label do nó alvo (`:Movie`) e a propriedade que será vetorizada (`tagline`).
    
- **Dimensões e Similaridade:** Para o modelo da OpenAI, utilizamos **1536 dimensões** e a métrica de **Similaridade de Cosseno**.
    

---

## 3. Pipeline de Ingestão: Vetorizando Propriedades

Diferente de um RAG vetorial puro, aqui os embeddings são armazenados como **propriedades do nó** no próprio Neo4j.

- **Função `genai.vector.encode`:** Esta função nativa (ou via plugin APOC) envia o texto para a API da OpenAI e armazena o array resultante no nó.
    
- **Parâmetros de Query:** O token de API é passado como parâmetro para garantir a segurança e conformidade.

```python
MATCH (m:Movie) WHERE m.tagline IS NOT NULL
WITH m
// Gera o embedding para cada tagline
CALL genai.vector.encode(m.tagline, "OpenAI", {token: $openAIKey}) YIELD vector
SET m.taglineEmbedding = vector // Armazena o vetor no nó

```

## 4. Recuperação Semântica (Vector Search no Grafo)

A busca ocorre em duas etapas integradas em uma única query Cypher:

1. **Vetorização do Prompt:** A pergunta do usuário é convertida em um embedding.
    
2. **Busca `top-K`:** O banco compara o vetor da pergunta com os vetores armazenados no índice e retorna os vizinhos mais próximos (nós com maior similaridade semântica).

```python
// Busca as 5 movies mais próximas semanticamente à pergunta
CALL db.index.vector.queryNodes('movie_tagline_embeddings', $topK, $questionEmbedding)
YIELD node AS movie, score
RETURN movie.title, movie.tagline, score
```

## Análise de Engenharia: O Valor do GraphRAG

Ao integrar vetores no grafo, resolvemos gargalos discutidos anteriormente:

- **Contextualização Relacional:** No RAG vetorial padrão, recuperamos _chunks_ isolados. No GraphRAG, após encontrar o nó via vetor (ex: Tom Hanks), você pode usar o Cypher para navegar e trazer **metadados estruturados** (filmes, diretores, premiações) que não estavam no texto original.
    
- **Otimização de Custos:** Ao vetorizar apenas propriedades chave (como `taglines` ou `sumários`), reduzimos drasticamente o número de tokens no prompt comparado ao _Grid Chunking_ ou à vetorização de PDFs inteiros.
    
- **Redução de Alucinação:** A resposta do LLM pode ser ancorada ("grounded") na estrutura de fatos do grafo, usando o vetor apenas para a "porta de entrada" da consulta.