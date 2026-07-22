---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-10-31'
---

A busca por **keyword search** (correspondência de palavras-chave) é limitada. Se você procura por "comida italiana barata" e um documento usa a frase "pizza com bom preço", o keyword search pode falhar. Ele procura por correspondências literais.

A **Busca Semântica** (Semantic Search) resolve isso. Ela foca no **significado** e na **intenção** por trás da sua consulta, e não apenas nas palavras em si.

## A Mágica do "Embedding": Transformando Palavras em Pontos

Para que um computador entenda o "significado", ele não pode ler texto; ele precisa ler matemática. É aqui que entra o processo de **Embedding**.

1. **Modelo de Embedding:** Usamos um modelo de IA (como os da OpenAI, Google, etc.) que foi treinado em bilhões de textos.
    
2. **Tradução para Vetores:** Esse modelo atua como um "tradutor universal". Ele pega um pedaço de texto (seja a sua pergunta ou um documento da base de dados) e o transforma em um **vetor**: uma longa lista de números (ex: `[0.02, 0.45, -0.12, ..., 0.88]`).
    
3. **O Espaço Vetorial:** Cada vetor é, na verdade, um **ponto** em um "mapa" com milhares de dimensões (o Espaço Vetorial).
    

Nesse mapa, palavras e frases com significados similares são posicionadas próximas umas das outras.

- O ponto para "eu quero pizza" estará muito perto do ponto para "onde encontrar uma pizzaria".
    
- Ambos estarão muito longe do ponto para "física quântica".
    

## Como Medir a "Proximidade"?

Uma vez que sua pergunta ("eu quero pizza") é transformada em um ponto, o sistema precisa encontrar os pontos de documentos mais próximos a ele. Para isso, ele "compara vetores para gerar pontuações" usando diferentes métricas.

As três mais comuns são:

### 1. Similaridade de Cosseno (Cosine Similarity)

Esta é a métrica mais popular para busca de texto.

- **O que mede:** Mede o **ângulo** entre dois vetores.
    
- **Por que é útil:** Ela ignora a "magnitude" (o comprimento/tamanho) do vetor. Por exemplo, a frase "eu quero pizza" e a frase "eu realmente, com certeza absoluta, quero pizza" terão vetores de tamanhos diferentes, mas apontarão para a **mesma direção** no mapa (terão o mesmo significado). A similaridade de cosseno captura isso perfeitamente, resultando em um score alto (próximo de 1.0).
    

### 2. Distância Euclidiana (Euclidean Distance)

Esta é a "régua" que aprendemos na escola.

- **O que mede:** A distância em **linha reta** (a menor distância física) entre dois pontos no mapa.
    
- **Por que é menos usada para texto:** Ela é muito sensível à magnitude. As duas frases sobre pizza do exemplo anterior seriam consideradas "distantes" por essa métrica, o que não é o que queremos. É mais usada em áreas como visão computacional.
    

### 3. Produto Escalar (Dot Product)

Esta métrica é uma alternativa rápida que combina os dois conceitos.

- **O que mede:** É o resultado da multiplicação dos componentes dos vetores. Na prática, é o resultado da **Similaridade de Cosseno multiplicado pelas magnitudes** de ambos os vetores.
    
- **Por que é útil:** É computacionalmente muito rápido. Se todos os vetores forem "normalizados" (forçados a ter um comprimento de 1), o resultado do Produto Escalar se torna **idêntico** ao da Similaridade de Cosseno, dando o melhor dos dois mundos: velocidade e precisão semântica.
    

## Conclusão

A Busca Semântica é a tecnologia central por trás dos sistemas RAG (Retrieval-Augmented Generation) e de qualquer IA moderna que "entende" o que você pergunta. Ao transformar texto em pontos em um mapa (embedding) e medir a proximidade entre eles (similaridade), ela permite encontrar respostas relevantes mesmo quando as palavras não são idênticas.