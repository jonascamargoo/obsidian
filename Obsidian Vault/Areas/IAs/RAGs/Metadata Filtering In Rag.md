



In RAG, metadata filtering doesn't permorm retrieval, it narrows down results from other techiques based on user attributes, not query content.


basic tf scoring treats all words equally, whether they're common filler words or rare, meaningful terms. Solution: weight terms using "inverse document frequency" (IDF). Então, basicamente o problema da TF é que se um documento é mais longo, consequentemente vai haver mais incidências daquele termo no documento, o que não significa que ele seja mais relevante. O IDF resolve isso, com a fórmula de score. score = tf(word, doc) * log(total docs/docs containing word). The result is an idf value for each word that captures how rare it is across the knowledge


https://satyadeepmaheshwari.medium.com/inverted-index-the-backbone-of-modern-search-engines-8bfd19a9ff75

## Completar no final de semana...


