---
tipo: aula
area: IAs
tags:
- ia/rag
- ia/knowledge-graph
criada: '2026-03-16'
---

Nesta sessão, traduzimos a teoria dos **Knowledge Graphs (KG)** para o código, utilizando o **Neo4j** como motor de banco de dados e o **LangChain** como interface de orquestração. Vamos trabalhar com um exemplo de filmes.
![[Pasted image 20260315213505.png]]

## 1. Configuração do Stack Tecnológico

Para iniciar o pipeline, utilizamos o `dotenv` para gerenciar segredos e a classe `Neo4jGraph` do LangChain para a abstração da conectividade.

```python
from dotenv import load_dotenv
import os
from langchain_community.graphs import Neo4jGraph
import warnings

# Silenciando warnings para um ambiente de produção limpo
warnings.filterwarnings("ignore")

# Carregamento de variáveis de ambiente (URI, User, Password, Database)
load_dotenv('.env', override=True)
NEO4J_URI = os.getenv('NEO4J_URI')
NEO4J_USERNAME = os.getenv('NEO4J_USERNAME')
NEO4J_PASSWORD = os.getenv('NEO4J_PASSWORD')
NEO4J_DATABASE = os.getenv('NEO4J_DATABASE')

# Inicialização da instância do grafo
kg = Neo4jGraph(
    url=NEO4J_URI, username=NEO4J_USERNAME, password=NEO4J_PASSWORD, database=NEO4J_DATABASE
)

```

## 2. Consultas Básicas e Introspecção do Grafo

O Cypher utiliza padrões visuais para encontrar dados. O fluxo básico consiste em definir a query e executá-la via `kg.query()`.

### A. Contagem e Agregação

Ao retornar dados, o LangChain formata o resultado como uma lista de dicionários, onde as chaves são os nomes definidos no `RETURN`.

```python
# Contagem total de nós para verificar a escala do dataset
cypher = "MATCH (n) RETURN count(n) AS numberOfNodes"
result = kg.query(cypher)
print(f"Existem {result[0]['numberOfNodes']} nós no grafo.")
```

### B. Filtragem por Labels e Nomes

A tipagem em grafos é feita por labels. A legibilidade é crucial, então usamos aliases semânticos (ex: `m` para `Movie`).

```python
# Buscando um nó específico por propriedade de valor exato
cypher = """
MATCH (tom:Person {name: "Tom Hanks"}) 
RETURN tom
"""
kg.query(cypher)
```

## 3. Lógica Condicional e Travessia de Relacionamentos

A principal vantagem do KG sobre o RAG vetorial é a eficiência em resolver relacionamentos complexos sem a latência de múltiplos cálculos de similaridade.

### A. Filtros com Cláusula WHERE

Para consultas que envolvem intervalos (como anos de lançamento), usamos o `WHERE`.

```python
cypher = """
MATCH (nineties:Movie) 
WHERE nineties.released >= 1990 AND nineties.released < 2000 
RETURN nineties.title
"""
kg.query(cypher)
```

### B. Pattern Matching Multimodal (Ator-Filme-Coadjuvante)

Podemos descrever sentenças inteiras de dados para encontrar conexões profundas. O padrão abaixo identifica co-atores que trabalharam com Tom Hanks.

```python
cypher = """
MATCH (tom:Person {name:"Tom Hanks"})-[:ACTED_IN]->(m)<-[:ACTED_IN]-(coActors) 
RETURN coActors.name, m.title
"""
kg.query(cypher)
```

## 4. Evolução do Grafo: Mutação e Idempotência

Para o seu curso, é vital ensinar como manter a integridade dos dados durante a ingestão.

- **Remoção de Relacionamentos:** Para corrigir inconsistências (como um ator listado erroneamente em um filme), deletamos apenas a aresta, preservando os nós.
    
- **Merge (Idempotência):** Em pipelines de ingestão automatizados, o `MERGE` é preferível ao `CREATE`, pois evita a duplicação de entidades se elas já existirem no banco.

```python
# Exemplo de criação de relação garantindo unicidade
cypher = """
MATCH (andreas:Person {name:"Andreas"}), (emil:Person {name:"Emil Eifrem"})
MERGE (andreas)-[rel:WORKS_WITH]->(emil)
RETURN andreas, rel, emil
"""
kg.query(cypher)
```

## ⚖️ Análise do Engenheiro: RAG Vetorial vs. GraphRAG

Com base neste material prático e nos arquivos de arquitetura anteriores:

1. **Densidade de Dados:** Enquanto o _Grid Chunking_ resolve a visualização de PDFs densos, o KG permite que o LLM entenda as entidades extraídas desses PDFs como registros interligados, não apenas como pedaços de texto.
    
2. **Segurança (RBAC):** O Cypher permite filtrar subgrafos inteiros programaticamente, oferecendo um controle de acesso mais robusto que os simples metadados de um banco vetorial.
    
3. **Hibridismo:** O próximo passo evolutivo para sua aula será converter as propriedades `title` e `tagline` em **vetores**, permitindo buscas semânticas dentro da estrutura de grafos que acabamos de construir.

