---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

## O que é?

Quando duas ou mais chaves geram o mesmo
endereço da Tabela Hash, dizemos que houve uma
colisão. Em aplicações práticas é difícil conseguir evitar o
problema de colisão de chaves.

## Principais causas:
*  em geral o número N de chaves possíveis é muito maior que o número de entradas disponíveis na tabela.
* não se pode garantir que as funções de hashing possuam um bom potencial de distribuição (espalhamento).

## Tratamento de colisões

* Um bom método de resolução de colisões é essencial, não importando a qualidade da função de hashing.
Há diversas técnicas de resolução de colisão. As técnicas mais comuns podem ser enquadradas em duas categorias: 

* Encadeamento : Nessa abordagem, cada posição da tabela hash contém uma estrutura de dados, como uma lista encadeada. Quando ocorre uma colisão, os elementos com a mesma chave hash são armazenados na mesma posição, formando uma lista encadeada. Dessa forma, vários valores podem ser associados à mesma posição na tabela. A busca de um elemento requer percorrer a lista encadeada correspondente;

* Endereçamento Aberto (Rehash): Nessa abordagem, quando ocorre uma colisão, são feitas tentativas para encontrar uma nova posição na tabela para o elemento colidido. Existem diferentes técnicas de endereçamento aberto, como o rehashing linear, em que é feito um deslocamento sequencial para encontrar uma posição vazia na tabela; o rehashing quadrático, em que a sequência de deslocamento é baseada em uma função quadrática; e o rehashing duplo, em que é utilizado um segundo hash para calcular o próximo endereço de tentativa (a distancia d agora é distância d²  no quadrático, logo joga ele pra mais longe diminuindo a probabilidade de colidir).


### Encadeamento

* A informação é armazenada em estruturas encadeadas fora da Tabela Hash. Coloca-se os elementos que possuem chaves iguais em uma lista encadeada. 
* No pior caso o tempo para inserir um novo elemento na tabela é O(1).
* Procurar por um elemento leva tempo proporcional ao tamanho da lista armazenada em cada slot.

![[Pasted image 20230715122517.png]]

### Endereçamento aberto (rehash)

* Elementos são armazenados na própria tabela hash: Não existe listas nem elementos armazenados fora da
tabela, evitando assim o uso de ponteiros.

* Vantagem: a quantidade de memória utilizada para armazenar ponteiros é utilizada para aumentar o tamanho da tabela, possibilitando menos colisões e aumentando a velocidade de recuperação das informações:

* Para inserir um novo elemento, examina-se sucessivamente a tabela até encontrarmos um slot vazio onde possamos armazenar o elemento. Um ponto importante é que não percorre-se a tabela inteira, isto é, a busca depende do elemento a ser inserido.

* A busca por um elemento deve seguir a mesma sequência de slots que o algoritmo que inseriu o elemento

#### Alguns problemas com endereçamento aberto são:

* Não podemos armazenar mais elementos que o tamanho máximo da tabela;
*  Remover um elemento é uma tarefa cara e difícil.
* Para remover um elemento de um slot i não podemos simplesmente marcar tal slot como VAZIO, pois isto tornaria impossível recuperar qualquer elemento cuja inserção encontrou o slot i ocupado. Uma alternativa seria marcar i como REMOVIDO ao invés de VAZIO (implica na modificação do algoritmo de busca e inserção).
* Quatro estratégias que utilizam a ideia de endereçamento aberto: Rehash Linear, Rehash Quadrática e Rehash Duplo.

#### Rehash linear

O rehash linear é uma técnica usada em tabelas de dispersão (hash tables) para lidar com colisões. Quando duas chaves diferentes têm o mesmo valor hash e precisam ser inseridas na mesma posição da tabela, ocorre uma colisão. O rehash linear é uma estratégia simples para resolver esse problema.

No rehash linear, quando ocorre uma colisão, a tabela de dispersão é percorrida sequencialmente a partir da posição de colisão até encontrar uma posição vazia onde a chave pode ser inserida. Essa busca linear é feita adicionando um valor fixo, geralmente 1, à posição atual a cada iteração.

Aqui está um exemplo simplificado do processo de rehash linear:

1. Uma chave é inserida na tabela de dispersão.
2. O valor hash da chave é calculado.
3. Se a posição correspondente no array subjacente da tabela de dispersão está vazia, a chave é inserida nessa posição.
4. Caso contrário, ocorre uma colisão e a tabela é percorrida linearmente a partir dessa posição.
5. A cada iteração, o valor fixo é adicionado à posição atual.
6. O processo de busca continua até encontrar uma posição vazia para inserir a chave.
7. A chave é então inserida na posição encontrada.

Essa estratégia de rehash linear pode ser eficiente em tabelas de dispersão com baixa carga (poucas colisões), mas pode levar a um desempenho ruim quando a carga aumenta e muitas colisões ocorrem, resultando em longas sequências de busca.

Existem outras técnicas de resolução de colisões, como rehash quadrático, encadeamento separado (chaining), encadeamento aberto (open addressing) com sondagem linear ou sondagem dupla, entre outras. Cada técnica tem suas vantagens e desvantagens, e a escolha depende do cenário específico e dos requisitos do sistema.

* Uma das alternativas mais usadas para aplicar Endereçamento Aberto é chamada de rehash linear. A posição na tabela é dada por:
* rh (k,i) = (h (k) + i) % tablesize, onde tablesize é a quantidade de entradas na Tabela Hash
	* k é a chave
	* i é o índice de reaplicação do Hash



#### Rehash quadrático

O rehash quadrático é outra técnica utilizada para resolver colisões em tabelas de dispersão (hash tables). Ao contrário do rehash linear, que realiza uma busca linear sequencial por uma posição vazia, o rehash quadrático utiliza uma função quadrática para determinar a próxima posição a ser verificada em caso de colisão.

A ideia básica do rehash quadrático é adicionar um incremento quadrático à posição original de colisão para encontrar a próxima posição a ser verificada. A função quadrática utilizada é geralmente da forma h(k, i) = (h'(k) + c1 * i + c2 * i^2) % tablesize, onde h'(k) é o valor hash original da chave k, i é o número da iteração e tablesize é o tamanho da tabela de dispersão.

Aqui está um exemplo simplificado do processo de rehash quadrático:

1. Uma chave é inserida na tabela de dispersão.
2. O valor hash da chave é calculado.
3. Se a posição correspondente no array subjacente da tabela de dispersão está vazia, a chave é inserida nessa posição.
4. Caso contrário, ocorre uma colisão e a função quadrática é usada para determinar a próxima posição a ser verificada.
5. A cada iteração, o valor de i é incrementado e a função quadrática é recalculada para obter a nova posição.
6. O processo de busca continua até encontrar uma posição vazia para inserir a chave ou até que um número máximo de iterações seja alcançado.

O rehash quadrático geralmente oferece uma melhor dispersão dos elementos colididos do que o rehash linear, reduzindo a formação de longas sequências de busca. No entanto, é importante ajustar adequadamente os valores de c1 e c2 na função quadrática para evitar agrupamento excessivo de elementos em determinadas posições.

É importante mencionar que o rehash quadrático também pode apresentar desvantagens, como a possibilidade de entrar em ciclos infinitos em determinadas situações. Para mitigar esse problema, é comum utilizar outras técnicas, como sondagem dupla (double hashing), em conjunto com o rehash quadrático.

Em resumo, o rehash quadrático é uma estratégia de resolução de colisões que utiliza uma função quadrática para determinar a próxima posição a ser verificada em caso de colisão. Essa técnica ajuda a reduzir a formação de longas sequências de busca, melhorando a eficiência das tabelas de dispersão.

#### Rehash duplo

O rehash duplo é uma técnica utilizada para resolver colisões em tabelas de dispersão (hash tables). Ao contrário do rehash linear e rehash quadrático, que utilizam incrementos fixos para determinar a próxima posição a ser verificada em caso de colisão, o rehash duplo utiliza uma função de hash secundária para calcular o passo de incremento.

A ideia básica do rehash duplo é utilizar uma segunda função de hash para calcular o incremento a ser adicionado à posição original de colisão, caso ocorra uma colisão. Essa segunda função de hash é geralmente na forma h2(k), onde h2 é a função de hash secundária e k é a chave a ser inserida.

Aqui está um exemplo simplificado do processo de rehash duplo:

1. Uma chave é inserida na tabela de dispersão.
2. O valor hash da chave é calculado.
3. Se a posição correspondente no array subjacente da tabela de dispersão está vazia, a chave é inserida nessa posição.
4. Caso contrário, ocorre uma colisão e a função de hash secundária é usada para calcular o incremento a ser adicionado à posição original.
5. A posição original é incrementada pelo valor calculado pela função de hash secundária.
6. O processo é repetido até encontrar uma posição vazia para inserir a chave ou até que um número máximo de iterações seja alcançado.

A escolha da função de hash secundária é crucial para evitar agrupamento excessivo de elementos em determinadas posições. É importante que a função de hash secundária seja capaz de gerar uma sequência de incrementos que evite colisões repetitivas.

O rehash duplo ajuda a reduzir a formação de sequências de busca longas, distribuindo as chaves colididas de forma mais uniforme pela tabela de dispersão. No entanto, é necessário garantir que a função de hash secundária seja suficientemente independente da função de hash original para evitar agrupamentos e ciclos infinitos.

Em resumo, o rehash duplo é uma técnica de resolução de colisões que utiliza uma função de hash secundária para calcular o incremento a ser adicionado à posição original em caso de colisão. Essa técnica melhora a distribuição das chaves colididas pela tabela de dispersão e reduz a formação de sequências de busca longas:

	rh (k ,i) =(h 1 (k) +ih 2(k ) ) % tablesize,

onde h 1(x) e h 2(x) são funções hash auxiliares. O primeiro elemento (i=0) é colocado na posição h 1(x) , no caso de colisões, os novos elementos são espalhados de acordo com h 2(x) . Exemplo de funções hash auxiliares frequentemente utilizadas são:

	h1 (x) =x % tablesize
	h2 (x) =1+( x % m)

onde m é um número um pouco menor que tablesize (tablesize - 1 ou tablesize - 2)

### Alguns contras do uso de hashing

O Hash é uma estrutura de dados do tipo
dicionário:
– Não permite armazenar elementos repetidos.
– Não permite recuperar elementos sequencialmente
(ordenado).
Para otimizar a função Hash é necessário
conhecer a natureza e domínio da chave a ser
utilizada.