---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2026-07-23'
fonte: Anthropic
---

**Contextual Retrieval** é uma técnica da Anthropic para melhorar a etapa de recuperação em sistemas [[Retrieval-Augmented Generation (RAG)|RAG]], atacando um problema clássico do [[Chunking]]: quando um documento é quebrado em pedaços, cada _chunk_ perde a noção de onde estava no todo e vira um fragmento "solto".

> [!info] Ideia central
> Antes de gerar o [[Embedding]] de cada chunk, usa-se um LLM para **prepend** (colar no início) um pequeno trecho de contexto que explica o que aquele chunk é dentro do documento completo. O chunk deixa de ser um fragmento isolado e passa a carregar sua própria âncora de significado.

---
## O problema do chunk "solto"

Um chunk como *"A receita cresceu 3% no trimestre"* é ambíguo fora de contexto: qual empresa? qual trimestre? Ao ser vetorizado isolado, ele fica semanticamente pobre e é difícil de recuperar para a consulta certa — a busca não sabe a que ele se refere.

## As duas metades da técnica

- **Contextual Embeddings**: um LLM gera, para cada chunk, uma frase curta situando-o (ex.: *"Este trecho é do relatório do 2º trimestre de 2023 da ACME Corp; discute o crescimento de receita."*). Esse contexto é **prependado ao chunk** antes de gerar o embedding. O vetor resultante representa o chunk *já situado*.
- **Contextual BM25**: o mesmo chunk contextualizado também é indexado para busca léxica (BM25), não só vetorial. Assim os termos do contexto (nomes, datas) entram no índice de palavra-chave. Isso conecta a técnica ao [[Hybrid Search]] — combina-se busca densa (embeddings) com esparsa ([[Keyword Search|BM25]]).

## Pipeline completo

1. Quebrar o documento em chunks ([[Chunking]])
2. Para cada chunk, gerar o contexto com um LLM e prependá-lo
3. Gerar [[Embedding|embeddings]] dos chunks contextualizados **e** indexá-los no BM25
4. Na consulta, recuperar por ambas as vias e fundir os resultados ([[Hybrid Search]])
5. Aplicar [[Reranking]] no topo para refinar a ordem final

## Custo e viabilidade

Gerar um contexto por chunk com um LLM parece caro, mas roda **uma vez na indexação** (não a cada query) e é fortemente barateado por _prompt caching_: o documento inteiro fica em cache enquanto se geram os contextos de todos os seus chunks, pagando o texto-base uma vez só.

> [!note] Ganho reportado
> Segundo a Anthropic, os Contextual Embeddings reduzem a taxa de falha na recuperação em ~35%; somados ao Contextual BM25, ~49%; e com [[Reranking]] no topo, ~67%. Números do estudo original — validar no seu próprio conjunto antes de assumir.

## Quando usar

Vale quando os chunks perdem muito significado isolados — bases grandes, documentos densos e auto-referentes (relatórios financeiros, jurídicos, técnicos). Para bases pequenas que cabem inteiras na janela de contexto, o RAG pode nem ser necessário.
