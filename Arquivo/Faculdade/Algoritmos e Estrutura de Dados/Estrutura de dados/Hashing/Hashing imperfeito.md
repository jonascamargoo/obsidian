---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

Hashing imperfeito, também conhecido como colisões de hashing, ocorre quando duas ou mais chaves diferentes são mapeadas para a mesma posição na tabela hash. Isso pode acontecer devido a vários fatores, como o tamanho limitado da tabela hash em relação ao número de chaves a serem armazenadas ou a natureza das funções de hashing utilizadas. Quando ocorrem colisões, é necessário adotar estratégias para lidar com elas. As principais abordagens para tratar colisões em hashing imperfeito incluem:

1.   Encadeamento separado:
	 Nesse método, cada posição da tabela hash contém uma lista encadeada de elementos. Quando ocorre uma colisão, um novo elemento é simplesmente adicionado à lista correspondente à posição da tabela. Dessa forma, diferentes chaves podem ser armazenadas na mesma posição, evitando a perda de dados. No entanto, o encadeamento separado pode resultar em um desempenho ligeiramente mais lento devido à necessidade de percorrer a lista encadeada para buscar ou atualizar elementos;
2. Sondagem linear:
	 Nessa abordagem, quando ocorre uma colisão, o algoritmo de sondagem linear procura pela próxima posição disponível na tabela hash e insere a chave nessa posição. A sondagem linear continua verificando as posições subsequentes até encontrar uma posição vazia. Esse método é simples de implementar, mas pode levar a agrupamentos e problemas de desempenho quando muitas colisões ocorrem em sequência;
3. Sondagem quadrática:
	Similar à sondagem linear, a sondagem quadrática também procura por posições disponíveis após uma colisão. No entanto, em vez de verificar as posições sequencialmente, a sondagem quadrática utiliza uma sequência quadrática para determinar as próximas posições a serem verificadas. Essa técnica visa reduzir o agrupamento de chaves na tabela hash;

OBS: é importante ressaltar que é bem difícil não haver colisões e que, é uma boa ideia deixar uma tabela com 60% a 70% de ocupação mais ou menos, a fim de evitar colisões e agrupamentos

Existe chaves x e y diferentes e pertencentes a A, onde a função Hash utilizada fornece saídas iguais

![[Pasted image 20230707100826.png]]

#### Análise com exemplo

Suponha que queiramos armazenar as seguintes chaves: C, H, A, V, E e S em um vetor de P = 7 posições (0..6) conforme a seguinte função f(k) = k(código ASCII) % P. Tabela ASCII: C (67); H (72); A (65); V (86); E (69) e S (83). Ficaria assim:

![[Pasted image 20230707102113.png]]
