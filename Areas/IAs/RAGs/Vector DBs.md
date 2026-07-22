---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-11-02'
---

Em sistemas RAG de produção, a performance e a escalabilidade da recuperação de vetores são gargalos críticos.

- **O Problema:** Bancos de dados relacionais tradicionais (SQL) são péssimos para busca semântica, pois suas operações se assemelham ao ineficiente $O(N)$ k-NN (Busca Exata).
    
- **A Solução:** **Vector Databases** (Bancos de Dados Vetoriais).
    
- **Por quê:** São bancos de dados especializados, projetados desde o início para armazenar e consultar vetores de alta dimensionalidade. Eles são otimizados para implementar algoritmos **ANN (Approximate Nearest Neighbors)**, como o HNSW, gerenciando eficientemente a construção de grafos de proximidade e o cálculo de distâncias em escala.
    

---

## 🚀 O Fluxo de Ingestão e Indexação (Ex: Weaviate)

Antes que qualquer busca possa ocorrer, o banco de dados precisa ser configurado e populado. O processo é:

1. **Conexão:** Estabelecer conexão com a instância do banco de dados (local ou nuvem).
    
2. **Criação da "Collection":** Definir um "schema" (como uma tabela) para os dados (ex: uma collection `Article` com propriedades `title` e `body`).
    
3. **Definição do Vectorizer:** Este é um passo crítico. Ao criar a collection, você especifica qual **modelo de embedding (vectorizer)** será usado (ex: `text-embedding-ada-002`). O banco de dados usará isso automaticamente para vetorizar os dados na ingestão e as consultas na busca.
    
4. **Ingestão de Dados:** Inserir os documentos (ex: via `batch.addObject`). Durante este passo, o banco de dados:
    
    - Armazena os dados brutos (JSON).
        
    - Chama o **vectorizer** para criar os _dense vectors_ (para Semantic Search).
        
    - Cria _automaticamente_ um **inverted index** (para Keyword Search).
        
    - Atualiza o **índice ANN** (ex: o grafo HNSW) com os novos vetores.
        
	![[Pasted image 20251102150743.png]]
	![[Pasted image 20251102150858.png]]
---

## 🔍 O Fluxo de Consulta: Hybrid Search em Produção

O verdadeiro poder dos Vector Databases modernos é sua capacidade nativa de executar buscas complexas em uma única consulta. A maioria dos sistemas de produção usa **Hybrid Search**.

### 1. Consultas Individuais (Os Blocos de Construção)

- **Keyword Search:** Uma consulta BM25 que usa o _inverted index_ pré-construído para encontrar correspondências exatas de palavras-chave.
    ![[Pasted image 20251102151359.png]]
- **Semantic Search:** Uma consulta de texto que é _primeiro_ vetorizada pelo banco de dados (usando o _vectorizer_ definido na collection) e _depois_ usa o índice ANN (HNSW) para encontrar os vizinhos mais próximos.
    ![[Pasted image 20251102151250.png]]

### 2. Hybrid Search (O Padrão de Produção)

A busca híbrida executa ambas (Keyword e Semantic) em paralelo e funde os resultados.

- **Ponderação (Alpha):** Ao contrário do RRF (que se baseia em _rank_), a implementação descrita (ex: Weaviate) usa um parâmetro `alpha` para **ponderar os _scores_** antes da reclassificação.
    
- A fórmula é `alpha` para semântica e `(1-alpha)` para keyword.
    
- **Exemplo:** `alpha = 0.25` (conforme o texto) significa:
    
    - **25%** do score final vem da **Semantic Search**.
        
    - **75%** do score final vem da **Keyword Search (BM25)**.
    ![[Pasted image 20251102151506.png]]

Isso permite um equilíbrio ajustável entre a relevância de significado (semântica) e a precisão literal (keyword).

### 3. Filtros (Metadata Filtering)

Finalmente, os filtros de metadados são aplicados _sobre_ a consulta híbrida para restringir ainda mais os resultados com base em atributos (ex: `autor == "Ana"`).
![[Pasted image 20251102151525.png]]

---

### O Pipeline Completo (Resumo)

O fluxo de trabalho de ponta a ponta em um Vector Database é:

1. **Configurar:** Definir a `collection` e o `vectorizer`.
    
2. **Carregar e Indexar:** Ingerir os dados. O banco de dados cuida automaticamente da vetorização (HNSW) e da indexação de palavras-chave (inverted index).
    
3. **Consultar:** Executar uma única chamada de API que combina:
    
    - **Hybrid Search** (com ponderação `alpha`).
        
    - **Metadata Filters**.