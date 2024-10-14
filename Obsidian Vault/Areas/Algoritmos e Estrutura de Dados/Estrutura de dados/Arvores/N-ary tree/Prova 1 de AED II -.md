

3)

A operação de exclusão entre vetores e árvores se diferem, pois um vetor é uma estrutura de dados linear e não hierárquica. Para se excluir um elemento, devemos primeiramente encontrá-lo e, após isso, ajustar o ponteiro, a ponto de referenciar corretamente o valor. Seria como o elemento seguinte tivesse de referenciar o anterior, fazendo isso para todas as posições seguintes. A complexidade dessa operação em um vetor é O(n), tendo seu pior caso ao percorrer um vetor completamente desordenado. Percebe-se que essa complexidade é considerada quando não se tem o índice da posição desejada e, caso tenha, o trabalho seria apenas referenciar corretamente os elementos subsequentes.

Em relação às árvores, a operação de exclusão requer a análise de alguns fatores a mais. Primeiramente, se caso o nó seja uma folha, ele pode ser deletado imediatamente. Se possuir um filho, só poderá ser removido após seu nó pai apontar o filho do nó filho a ser excluído. A complexidade da operação em questão é O(logN) em árvores balanceadas e, em caso de uma árvore não balanceada, pode ser considerado O(h), em que h é a profundidade do nó desejado. Essa complexidade ocorre pois o caráter logarítmico vem da busca binária.

O pior caso de inserção no vetor é quando o elemento deve ser inserido no início, pois todos os outros deverão ser deslocados, isto é, referenciar o próximo elemento. Já em relação à árvore, o pior caso ocorre quando estamos tentando excluir um elemento menor ou maior que todos os outros, pois aí temos de percorrer ambas extremidades esquerda e direita, respectivamente.

1)

  

A operação de inserção em um vetor pode possuir complexidades diferentes, a depender da posição de inserção. No início, é onde temos o pior caso, pois todos  elementos do vetor devem ser deslocados. Já sobre as  árvores, devemos percorrê-la em complexidade O(logN), caso esteja balanceada. E, caso não esteja, seria O(n). Percebe-se que a dificuldade aqui está em percorrer a árvore.

O pior caso de inserção no vetor é quando o elemento deve ser inserido no início, pois todos os outros deverão ser deslocados, isto é, referenciar o próximo elemento. Já em relação à árvore, o pior caso ocorre quando estamos tentando excluir um elemento menor ou maior que todos os outros, pois aí temos de percorrer ambas extremidades esquerda e direita, respectivamente.

  

2)

Uma árvore com uma altura muito elevada requer mais uso de memória, pois a quantidade de nós aumenta consideravelmente nesse caso. Os dados são inseridos na memória primária, que é significantemente mais rápida. Em caso que a árvore não caiba na memória RAM, ela deve ser armazenada na memória secundária, lenta. Isso gera uma queda na gigante na execução do programa em questão.

Algoritmos recursivos são geralmente mais caros e ineficientes, porém mais elegantes. Apesar disso, sua utilização é discutível em alguns casos em que se tenha que usar outra estrutura de dados, como uma pilha, para auxiliar nas operações, principalmente quando a estrutura de dados auxiliar pode ser muito grande. No caso do algoritmo recursivo, ele utiliza a própria call stack como estrutura de dados. Vamos supor que temos de definir um tamanho fixo para a pilha auxiliar na abordagem iterativa e, com isso, haja alguma quantidade de memória alocada que não foi utilizada. Esse cenário descrito anteriormente representa um caso em que talvez a abordagem recursiva seria melhor, já que o próprio sistema operacional gerencia a stack. Dito isso, essa vantagem depende, obviamente, do programador que está lidando com o caso.

**