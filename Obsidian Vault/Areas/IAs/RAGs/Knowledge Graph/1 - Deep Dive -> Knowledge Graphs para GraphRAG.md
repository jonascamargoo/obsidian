
O uso de Grafos de Conhecimento (KGs) representa uma evolução na forma como estruturamos a base de conhecimento para LLMs. Enquanto o RAG tradicional utiliza representações vetoriais densas (embeddings) para busca por similaridade, o GraphRAG utiliza a **relação explícita** entre entidades para fornecer contexto estruturado.

## 1. O Modelo de Grafo de Propriedades (Property Graph)

![[Pasted image 20260315212059.png]]

### A. Nós (Entidades como Registros)

Nós representam os objetos ou entidades do domínio.

- **Labels:** São utilizados para agrupar nós (ex: `:Person`, `:Course`). Labels funcionam como "classes" em POO.
    
- **Properties:** São pares chave-valor armazenados no nó (ex: `name: "Andreas"`, `id: 123`).
    
- **Representação Textual:** No padrão Cypher, utilizamos parênteses para representar nós: `(p:Person {name: "Andreas"})`.
    

### B. Relacionamentos (Arestas com Semântica)

Diferente de um banco relacional onde as relações são inferidas via JOINs, no KG as relações são **registros de dados explícitos**.

- **Direção e Tipo:** Todo relacionamento possui uma direção (origem $\to$ destino) e um tipo (ex: `[:TEACHES]`, `[:KNOWS]`).
    
- **Propriedades de Aresta:** Relacionamentos também carregam dados (ex: `since: 2024`), permitindo consultas temporais ou ponderadas.
    
- **Representação Textual:** `(Andreas)-[:TEACHES {year: 2024}]->(Course)`.
    

---

## 2. Modelagem Estratégica: Roles vs. Relationships

Um ponto crucial de engenharia discutido no vídeo é a **economia de labels**.

- **Anti-padrão:** Criar labels estáticos como `:Teacher` ou `:Student`.
    
- **Padrão Recomendado:** Definir o papel da entidade através da **relação**. Andreas é um "professor" porque existe uma aresta `[:TEACHES]` saindo dele para um curso.
    
- **Vantagem:** Isso reduz a redundância de dados e permite que uma entidade assuma múltiplos papéis dinamicamente sem alterar sua estrutura base.
    

---

## 3. Integração: Por que usar Grafos no seu Pipeline RAG?

Conectando os fundamentos do vídeo com os desafios técnicos dos seus arquivos de backend:

### A. Resolvendo o Desafio da Densidade

Arquivos como PDFs e slides possuem alta densidade de informação, onde um único vetor pode falhar em capturar todas as nuances.

- **Solução com KGs:** Em vez de usar _Grid Chunking_ puramente visual, o GraphRAG mapeia entidades dentro do PDF (ex: "Gráfico X" $\to$ `[:REPORTS]` $\to$ "Métrica Y"). Isso permite que o LLM navegue por fatos interligados em vez de apenas buscar quadrados de pixels.
    

### B. Segurança e Controle de Acesso (RBAC)

A segurança em bancos vetoriais é complexa devido à necessidade de vetores descriptografados na memória para o algoritmo ANN.

- **Vantagem do Grafo:** É possível aplicar controle de acesso granular em nível de **nó** ou **aresta**. Se um usuário não possui permissão para o label `:Finance`, o motor de busca do grafo (Cypher) simplesmente ignora esse subgrafo durante a recuperação, garantindo um isolamento mais robusto que simples filtros de metadados.
    

### C. Latência e Performance

Quase toda a latência de um RAG vem dos Transformers.

- **Otimização:** Consultas Cypher bem estruturadas no GraphRAG podem ser mais rápidas que buscas vetoriais em larga escala, pois o grafo limita o espaço de busca através das conexões, reduzindo a necessidade de modelos de _Reranking_ pesados para filtrar ruído.
    

---

## 🛠️ Exemplo de Implementação: Cypher Query

Para recuperar o contexto de quem introduziu uma seção do curso "RAG com Knowledge Graphs", o engenheiro de AI utilizaria a linguagem **Cypher**:

Cypher

```
MATCH (p:Person)-[:INTRODUCED]->(c:Course {name: "RAG with Knowledge Graphs"})
RETURN p.name, c.section
```

---

## 📈 Tabela Comparativa: Vector RAG vs. GraphRAG

|**Característica**|**Vector RAG (Semantic Search)**|**GraphRAG (Structured Retrieval)**|
|---|---|---|
|**Busca**|Similaridade de Cosseno / Distância Euclidiana|Travessia de Grafo / Padrões Cypher|
|**Contexto**|Fragmentos (Chunks) isolados|Entidades e suas interconexões|
|**Pontos Fortes**|Dados não estruturados, linguagem natural|Dados densos, regras de negócio, linhagem|
|**Custo de RAM**|Alto (Índices HNSW)|Proporcional ao número de nós/arestas|

---

### 🚀 Próximo Passo para o Material do Curso