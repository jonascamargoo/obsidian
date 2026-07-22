---
tipo: conceito
area: Linguagens Formais e Autômatos
tags:
- compiladores/linguagens-formais
criada: '2024-10-14'
---

## Conceitos básicos de linguagens
### Palavras
 As palavras são compostas por sequências de caracteres válidos, que podem ser letras, números, símbolos de pontuação, entre outros, a depender da linguagem e do contexto. Além disso, é finita.
### Alfabeto
Conjunto de caracteres, que podem ou não ser finitos. O mandarim não é, enquanto o português é.
### Linguagens
Conjunto de palavras
### Linguagem regular
No contexto da computação, uma linguagem é dita regular se puder se reconhecida por um autômato
### Linguagens Formais
Uma linguagem formal é um conjunto abstrato de **strings** (sequências finitas de símbolos) definidas por regras matemáticas precisas. Essas regras determinam quais strings são válidas na linguagem e quais não são.

As linguagens formais são ferramentas poderosas para modelar diferentes aspectos da linguagem natural, como a sintaxe e a semântica. Elas permitem que os linguistas e os cientistas da computação estudem a linguagem de forma rigorosa e precisa, além de desenvolverem ferramentas para processá-la e analisá-la.

## O que são Autômatos

Um autômato é um modelo matemático que reconhece e gera strings em uma linguagem formal. Ele é representado por uma máquina abstrata com **estados**, **regras de transição** e um mecanismo de **entrada** e **saída**. Em suma, uma máquina.

O autômato lê a string de entrada símbolo por símbolo e, a cada símbolo, ele muda de estado de acordo com as regras de transição. Se a string levar o autômato a um estado final, ela é considerada válida na linguagem formal. Caso contrário, a string/linguagem é inválida.

FALAR SOBRE LAMBDA E O VAZIO
### Exemplos

#### 1 - Linguagem L1: palavras representam pares em binário.

Pares em binário são representados por valores terminados em 0. Seja P parada e I início:

		![[Pasted image 20240402184217.png]]

#### 2 - Linguagem L2: Palavras tem tamanho par

Seja TP tamanho par e TI tamanho ímpar, com o alfabeto {a, b}:

		![[Pasted image 20240402184819.png]]

#### 3 - Linguagem L3: Palavras tem tamanho par, exceto lambda

Seja TP tamanho par e TI tamanho ímpar, com o alfabeto {a, b} e lambda como vazio:

		![[Pasted image 20240402185124.png]]

#### 4 - Linguagem L4: Palavras que representam não pares 

		![[Pasted image 20240402191225.png]]


#### 5 - Linguagem L5: palavras ímpares em binário

		![[Pasted image 20240402193448.png]]


#### 6 - Linguagem L5: representa par e |w| >= 3




#### 7 - Faça um AFD que aceite palavras da seguinte linguagem L = {w ∈ {0,1}* | todo '1' é imediatamente seguido por três '0'; e nunca há mais que quatro '0' consecutivos}.


		![[Pasted image 20240402203832.png]]




#### 8 - Faça um AFD que aceite palavras da seguinte linguagem L = {u,v,w ∈ {a,b,c}* | palavras têm o formato uaavbbwcc }.

		![[Pasted image 20240402210729.png]]



exemplo de palavra para essa linguagem: 

	a*aa*bbbaacccaa*bb*aabbccccccaaabb*cc*, entao basicamente tudo que está antes do *aa* é o "u", tudo entre *aa* e *bb* é "v" e tudo entre *bb* e *cc* é considerado "w" 

#### 8 - Faça um AFD que aceite palavras da seguinte linguagem L = {w ∈ {0,1,2}* | w possui pelo menos três '0', pelo menos um '1', e pelo menos dois '2'}.





Muito grande pra terminar. Mas o caminho é esse... REFAZER



_______________________RASCUNHO




## Tipos de Autômatos

Existem diversos tipos de autômatos, cada um com suas características e capacidades específicas. Os mais comuns são:

- **Autômatos Finitos Determinísticos (AFDs):** Possuem um único estado para cada símbolo da linguagem e regras de transição determinísticas.
- **Autômatos Finitos Não Determinísticos (AFNDs):** Possuem um conjunto de estados para cada símbolo da linguagem e regras de transição não determinísticas.
- **Autômatos com Pilha (APs):** Possuem uma pilha para armazenar símbolos e regras de transição que dependem do conteúdo da pilha.
- **Máquinas de Turing:** São modelos computacionais abstratos que podem ser usados para definir qualquer linguagem formal.

**Aplicações de Linguagens Formais e Autômatos:**

As linguagens formais e os autômatos têm diversas aplicações práticas em diferentes áreas do conhecimento, como:

- **Compiladores de linguagens de programação:** Os compiladores traduzem programas escritos em linguagens de alto nível para a linguagem de máquina que os computadores podem entender. Para isso, eles usam autômatos para analisar a sintaxe do programa e gerar o código de máquina equivalente.
- **Ferramentas de análise de código:** As ferramentas de análise de código verificam se o código de um programa está correto e se ele segue as boas práticas de programação. Para isso, elas usam autômatos para analisar a estrutura do código e identificar possíveis erros.
- **Tradutores automáticos:** Os tradutores automáticos traduzem textos de um idioma para outro. Para isso, eles usam autômatos para analisar a sintaxe do texto original e gerar o texto traduzido.
- **Sistemas de reconhecimento de voz:** Os sistemas de reconhecimento de voz convertem a fala humana em texto. Para isso, eles usam autômatos para analisar os sons da fala e identificar as palavras que foram pronunciadas.
- **Modelagem de protocolos de comunicação:** Os protocolos de comunicação definem as regras que os computadores usam para se comunicar entre si. As linguagens formais e os autômatos podem ser usados para modelar esses protocolos e verificar se eles estão corretos.