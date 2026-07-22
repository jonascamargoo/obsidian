---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-11-02'
---

Embora os Vector Databases sejam otimizados para a recuperação de vetores em escala, a _performance_ e a _qualidade_ de um sistema RAG dependem criticamente de como os dados são preparados. A primeira e mais importante adaptação é o **Chunking** (ou fragmentação).

**Chunking** é a prática de quebrar documentos longos (ex: livros, artigos) em pedaços menores (chunks) antes da vetorização.

---
## A Otimização Fundamental de Pré-processamento

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

## Estratégias Avançadas de Chunking (Pós-Prototipagem)

Embora o chunking de tamanho fixo ou recursivo (baseado em caracteres) seja um bom ponto de partida para prototipagem, ele é "agnóstico" ao conteúdo e pode falhar em preservar a coesão semântica.

O problema é que uma divisão arbitrária pode quebrar o contexto. O exemplo do texto é claro: um chunk contendo "...ela era finalmente uma campeã olímpica" pode ter seu significado completamente distorcido se o início ("Naquela noite ela sonhou...") for cortado.

Para resolver isso, as técnicas avançadas de chunking tentam criar fragmentos com base no **significado** do texto, e não em seu comprimento.

---

### 1. Semantic Chunking (Baseado em Distância Vetorial)

Esta técnica agrupa sentenças com base em sua similaridade semântica.

- **Como Funciona:** O algoritmo move-se pelo documento sentença por sentença.
    
- **O Processo:**
    
    1. O algoritmo mantém um "chunk em crescimento" (inicialmente, a primeira sentença).
        
    2. Ele vetoriza o **chunk atual** e a **próxima sentença** da fila.
        
    3. Ele calcula a distância vetorial (ex: dissimilaridade de cosseno) entre os dois.
        
    4. **Decisão:**
        
        - **Se `distância < threshold`:** Os textos são semanticamente similares. A sentença é adicionada ao chunk atual, e o processo se repete com a próxima sentença.
            
        - **Se `distância > threshold`:** A próxima sentença é considerada um novo tópico. O chunk atual é "cortado" (finalizado), e um novo chunk é iniciado com essa nova sentença.
            
- **Resultado:** Chunks de tamanho variável que tendem a seguir o "fluxo de pensamento" do autor. Se o autor divaga ou muda de tópico, um novo chunk é criado.
    ![[Pasted image 20251102160328.png]]
    
- **Trade-off:**
    
    - **Pró:** Alta qualidade de recuperação (Precision/Recall), pois os conceitos são mantidos coesos.
        
    - **Contra:** Computacionalmente caro na ingestão, pois exige vetorizações repetidas a cada sentença.
        

---

### 2. Chunking Baseado em LLM (Baseado em Instrução)

Esta abordagem trata o chunking como uma tarefa de geração de texto.

- **Como Funciona:** Você "pede" a uma LLM para fazer o chunking por você através de um prompt.
    
- **O Processo:**
    
    1. Você fornece o documento inteiro para uma LLM.
        
    2. Você fornece instruções, como: "Separe este texto em chunks. Mantenha conceitos similares juntos e crie um novo chunk quando um novo tópico for discutido."
        
    3. A LLM "lê" o texto e gera os chunks formatados como saída.
	    ![[Pasted image 20251102160433.png]]
- **Trade-off:**
    
    - **Pró:** Potencialmente o método de maior performance, pois pode capturar nuances que até o semantic chunking perderia.
        
    - **Contra:** É inerentemente uma "caixa-preta" (difícil de auditar) e seu custo (econômico e de tempo) pode ser proibitivo, embora esteja se tornando mais viável.
        

---

### 3. Otimização: Context-Aware Chunking (Enriquecimento via LLM)

Esta não é uma estratégia de _chunking_ em si, mas uma **melhoria** que pode ser aplicada _sobre_ qualquer método (fixo, recursivo, semântico, etc.).

O objetivo é resolver o problema de chunks que, mesmo semanticamente coesos, não têm contexto (ex: um chunk que é apenas uma longa lista de nomes).

- **Como Funciona:** Após a criação dos chunks, uma LLM é usada para adicionar contexto a cada um.
    
- **O Processo:** Para cada chunk, a LLM é instruída a adicionar um texto de resumo.
    
    - **Exemplo:** O chunk `[...lista de nomes...]` é transformado em `[Contexto: Este chunk lista os contribuidores e apoiadores que o autor agradece no final do post. Lista: ...lista de nomes...]`.
        ![[Pasted image 20251102160726.png]]
- **O Benefício Duplo (Ponto-Chave):**
    
    1. **Na Indexação:** O texto adicionado ("Contexto: ...") faz parte do chunk quando ele é **vetorizado**. Isso torna o vetor muito mais "rico" e melhora drasticamente a relevância da busca (o vetor agora "sabe" que é uma lista de agradecimentos).
        
    2. **Na Geração:** Quando o chunk é recuperado, o texto de contexto também é enviado para a LLM final, ajudando-a a entender _o que_ ela está lendo.
        
- **Trade-off:**
    
    - **Pró:** Grande aumento na relevância da busca e na qualidade da geração final.
        
    - **Contra:** Processo de ingestão (pré-processamento) extremamente caro, pois requer uma chamada de LLM para _cada chunk_ da sua base.
        
    - **Ponto Positivo:** Não tem **nenhum impacto** na velocidade da _busca_ (o custo é pago apenas na ingestão).
        

---

## Estratégia e Conclusão

O objetivo do engenheiro de RAG não é usar a técnica mais avançada, mas sim a mais adequada para o custo-benefício do projeto.

1. **Prototipagem:** Comece com **fixed-size** ou **recursive character splitting**. São bons padrões e fáceis de implementar.
    
2. **Otimização 1 (Validar):** Se a relevância da busca for um problema, teste **Semantic Chunking** ou **LLM-based Chunking** _em um subconjunto_ dos seus dados. Meça (com métricas como MAP e Recall) se o ganho de performance justifica o custo computacional de ingestão.
    
3. **Otimização 2 (Upgrade):** O **Context-Aware Chunking** é frequentemente um bom próximo passo, pois melhora tanto a recuperação (R) quanto a geração (G) do RAG, sem penalizar a latência da busca.