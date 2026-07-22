### Motivação

Até agora estudamos pesquisas sequenciais. Arranjos não fornecem mecanismos para calcular o índice a partir de uma informação armazenada. A pesquisa não é O(1). Exemplo, supondo um array em que há um string "maria" na posição 3. Eu não consigo, em O(1), saber onde ela está, sem varrer o array antes.

### Definição

Hash é uma generalização da noção mais simples de um arranjo comum, sendo uma estrutura de dados do tipo dicionário - Dicionários são estruturas especializadas em
prover as operações de inserir, pesquisar e remover. A ideia central do Hash é utilizar uma função, aplicada sobre parte da informação (chave), para retornar o índice onde a informação deve ou deveria estar armazenada. Podemos dizer de forma grosseira que tabelas hashing são estruturas de dados que contém outras estruturas de dados.

- Função de Hashing: função que mapeia a chave para um índice de um arranjo
- A estrutura de dados Hash é comumente chamada de Tabela Hash

![[Pasted image 20230706214429.png]]


* É uma estrutura de dados especial, que armazena as informações desejadas associando chaves de pesquisa a estas informações.

- Objetivo: a partir de uma chave, fazer uma busca rápida e obter o valor desejado.
A ideia central por trás da construção de uma Tabela Hash é identificar, na chave de busca, quais as partes que são significativas

### Como representar Tabelas Hash?

- Vetor: cada posição do vetor guarda uma informação. Se a função de hashing aplicada a um conjunto de elementos determinar as informações I 1 , I 2 , ..., I n , então o vetor 
   V[1... N] é usado para representar a tabela hash.

- Vetor + Lista Encadeada: o vetor contém ponteiros para as listas que representam as informações.

### Função de Hashing

- A Função de Hashing é a responsável por gerar um índice a partir de uma determinada chave.
- O ideal é que a função forneça índices únicos para o conjunto das chaves de entrada possíveis.
- A função de Hashing é extremamente importante, pois ela é responsável por distribuir as informações pela Tabela Hash.
- A implementação da função de Hashing tem influência direta na eficiência das operações sobre o Hash.

![[Pasted image 20230706220409.png]]


