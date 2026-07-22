---
tipo: conceito
area: Computer Organization and Architecture
tags:
- hardware
criada: '2024-10-14'
---

Imagina que eu esteja em uma biblioteca estudando sobre história do Brasil. Eu procuro por livros que fale do sec XIX, então toda hora vou à prateleira entregar e pegar outro em busca desse tópico, olhando para livros próximos. Ou seja, programas e pessoas tendem a acessar apenas uma pequena parte de sua memória ou coleção de livros de cada vez. É assim que computadores funcional. Programadores e sistemas de computador trabalham para criar a impressão de que possuem uma quantidade virtualmente ilimitada de memória rápida, mesmo que os recursos de hardware reais sejam limitados.
##### Localidade temporal
"If an item is referenced, it will tend to be referenced again soon".  If you recently brought a book to your desk to look at,
you will probably need to look at it again soon.
##### Localidade espacial
"If an item is referenced, items whose addresses are close by will tend to be referenced soon." Se buscamos um livro em uma seção, provavelmente pegaremos outro próximo em nossa pesquisa - para entender um tópico, precisamos entender os tópicos relacionados, portanto, pegaremos livros próximos.
###### stride-1 reference pattern

Quando acessamos sequencialmente. Por exemplo, ao percorrer um vetor em um loop `for` de `0` até `n-1`, acessando `vetor[i]`, onde `i` varia de `0` até `n-1`. Aqui, mantemos a row-major order
###### stride-k reference pattern

 Esse padrão ocorre quando você acessa apenas cada k-ésimo elemento do vetor. Em outras palavras, você pula k elementos entre cada acesso. Por exemplo, ao percorrer um vetor em um loop `for` de `0` até `n-1`, acessando `vetor[i * k]`, onde `i` varia de `0` até `(n-1)/k`. Isso é útil em situações onde você precisa acessar apenas um subconjunto dos elementos do vetor ou precisa processar os elementos de forma diferente com um intervalo fixo.