---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

### Como analisar problemas através de uma recursão

Para cada procedimento recursivo, associar uma
função de custo f(n) desconhecida (n mede o tamanho
dos argumentos)

– Obter uma relação de recorrência.
– Calcular a complexidade da relação de recorrência.

### recursão

Uma definição na qual o item que está sendo
definido aparece como parte da definição é
chamada definição indutiva ou definição recursiva.
Definições recursivas são compostas de duas
partes:

– Uma base, onde alguns casos simples do item que
está sendo definido são dados explicitamente;

– Um passo indutivo ou recursivo, onde outros casos do
item que está sendo definido são dados em termos dos
casos anteriores.

### sequencias recursivas

Uma sequência S é uma lista de objetos que são enumerados segundo alguma ordem; existe o 1º objeto, um segundo e assim por diante; S(k) denota o K-ésimo objeto da sequência.

Uma sequência é definida recursivamente, explicitando-se seu primeiro valor (ou seus
primeiros valores) e, a partir daí, definindo-se outros valores na sequência em termos dos
valores iniciais.

### relações de recorrência

As relações de recorrência são utilizadas para
descrever algoritmos recursivos. Uma recorrência é uma equação ou desigualdade
que descreve uma função em termos de entradas menores.

Existem três métodos principais para resolver relações de recorrência:

– Método da Substituição
– Método da Iteração
– Método Master ou Mestre

#### método da substituição

a ideia é jogar valores na recorrência até encontrar uma expressão que a defina, mas nao entraremos nela por ser ineficiente (literalmente tentativa e erro)

#### método da iteração

A ideia é expandir (iterar) a recorrência e expressá-la como uma soma de termos
dependentes apenas de n e das condições iniciais. Técnicas para avaliar somas podem então ser usadas para encontrar a solução.

exemplos de foto que tirei do caderno AQUI


#### método master

* O método Máster provê uma “receita” para resolver recorrências do tipo T(n) = a T(n/b) + f(n) com a ≥1, b>1 constantes e f(n) função assintoticamente positiva.

* A ideia da recorrência é a divisão de um problema de tamanho n em a subproblemas, cada um de tamanho n/b;

* Os a subproblemas são resolvidos de forma recursiva, cada um com tempo T(n/b);

* O custo de dividir o problema e combinar os resultados dos subproblemas é descrito pela função f(n);

* O método master nos dá a complexidade, nao a função completa em si. Só uma das 3 condições será satisfeita, portanto, as outras duas necessariamente deveram ser falsas.

##### teorema master

Seja T(n) = a T(n/b) + f(n) a≥1, b>1, f(n) ≥ 0 Então T(n) pode ser limitada assintoticamente como segue:

i. Se f(n) = O(n^((log a na base b) - ε ))  para alguma constante ε > 0, então T(n) = θ(n logba );

ii. Se f(n) = θ(n^(log a na base b), então T(n) = θ(n logba . log n);

iii.Se f(n) = Ω(n^((log a na base b) + ε )) para alguma constante ε > 0 e a.f(n/b) ≤ c.f(n) para alguma constante c < 1, então T(n) = θ(f(n)).