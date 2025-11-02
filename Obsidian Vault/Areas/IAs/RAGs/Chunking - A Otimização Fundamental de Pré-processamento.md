Embora os Vector Databases sejam otimizados para a recuperação de vetores em escala, a _performance_ e a _qualidade_ de um sistema RAG dependem criticamente de como os dados são preparados. A primeira e mais importante adaptação é o **Chunking** (ou fragmentação).

**Chunking** é a prática de quebrar documentos longos (ex: livros, artigos) em pedaços menores (chunks) antes da vetorização.

---

### Por que o Chunking é Crítico? (Os 3 Motivos)

1. **Limitação do Modelo de Embedding:** A maioria dos modelos (ex: `text-embedding-ada-002`) possui um limite máximo de tokens/texto que pode ser processado em uma única chamada. O chunking garante que nenhum pedaço de texto exceda esse limite.
    
2. **Otimização da Janela de Contexto (LLM):** O objetivo do RAG é fornecer ao LLM _apenas_ o contexto mais relevante. Recuperar um livro inteiro (50.000 tokens) para responder a uma pergunta específica é inviável e preencheria (ou estouraria) a janela de contexto da LLM, tornando a resposta impossível.
    
3. **Aumento da Relevância da Busca (O Motivo Principal):** Este é o ponto técnico mais importante.
    
    - **O Problema do "Vetor Médio":** Se você vetorizar um livro inteiro, você comprime o significado de milhares de tópicos, capítulos e páginas em um **único vetor**. Esse vetor representa a "média" semântica do livro.
        
    - **A Consequência:** Esse vetor "médio" não possui **especificidade semântica**. Se você perguntar sobre um tópico específico (ex: "o que acontece no Capítulo 5?"), o vetor da sua consulta não encontrará correspondência, pois o vetor do livro "diluiu" o significado do Capítulo 5 com todos os outros capítulos. A relevância da busca será péssima.
        

Ao quebrar o livro em 1 milhão de parágrafos (chunks), cada vetor representa um conceito específico e de forma "nítida". Os Vector Databases são projetados para escalar e lidar com esse aumento no número de vetores.

---

### O Trade-Off: Encontrando o Tamanho Ideal

O chunking é um exercício de equilíbrio (trade-off) entre especificidade e contexto.

- **Chunks Grandes (ex: por capítulo):** Você ainda sofre do problema do "vetor médio". O significado é muito amplo e o contexto enviado ao LLM é muito grande.
    
- **Chunks Pequenos (ex: por palavra ou frase):** O vetor perde todo o contexto semântico. O vetor para a palavra "rosa" não sabe se está falando de uma flor ou da cor, levando a uma relevância de busca igualmente ruim.
    

---

### Estratégias de Chunking (Algoritmos)

#### 1. Fixed-Size Chunking (Tamanho Fixo)

A abordagem mais simples.

- **Como:** Define um tamanho fixo (ex: 250 caracteres). Chunk 1 (1-250), Chunk 2 (251-500), etc.
    
- **Problema:** Quebras arbitrárias. É provável que o chunk termine no meio de uma palavra ou divida uma ideia coesa em dois chunks, destruindo o contexto.
    ![[Pasted image 20251102153729.png]]

#### 2. Fixed-Size com Overlap (Sobreposição)

A primeira melhoria.

- **Como:** Define um tamanho e uma sobreposição.
    
    - `Chunk 1:` Caracteres 1-250
        
    - `Chunk 2:` Caracteres 226-475 (com 25 de overlap)
        
    - `Chunk 3:` Caracteres 451-700 (com 25 de overlap)
    ![[Pasted image 20251102153813.png]]
- **Benefício:** Minimiza o problema da quebra arbitrária. O contexto no final do Chunk 1 também estará presente no início do Chunk 2. Isso aumenta a probabilidade de que um conceito seja mantido junto em pelo menos um chunk.
    
- **Trade-off:** Aumenta a redundância e o número total de vetores na base.
    

#### 3. Recursive Character Text Splitting (Chunking Estrutural)

Uma abordagem mais dinâmica e "content-aware" (sensível ao conteúdo).

- **Como:** Você define uma _hierarquia_ de caracteres separadores. O algoritmo tenta dividir pelo primeiro (ex: `\n\n` - novo parágrafo) e, se os chunks resultantes ainda forem muito grandes, ele os divide pelo próximo separador (ex: `\n` - nova linha), e assim por diante.
    
- **Benefício:** Respeita a estrutura do documento (parágrafos, listas), mantendo a coesão semântica.
    
- **Downside:** Pode criar chunks de tamanhos muito variáveis.
    
	![[Pasted image 20251102153855.png]]
#### 4. Chunking Semântico (Por Tipo de Documento)

A abordagem mais avançada, onde o chunking se adapta ao tipo de dados:

- **HTML:** Dividir por tags (`<p>`, `<div>`, `<h1-h6>`).
    
- **Código (ex: Python):** Dividir por classes ou definições de funções (`def`, `class`).
    
- **Documentos (ex: Markdown):** Dividir por cabeçalhos (`##`).
	![[Pasted image 20251102154025.png]]

---

### Considerações Finais

- **Metadados:** É fundamental que os chunks **herdem os metadados** do documento pai (ex: `source_url`, `author`, `doc_name`) e, opcionalmente, adicionem seus próprios (ex: `chunk_number`).
    
- **Ponto de Partida (Heurística):** Um bom ponto de partida, se não houver outra informação, é usar **fixed-size chunks de ~500 caracteres com um overlap de 50-100 caracteres**.