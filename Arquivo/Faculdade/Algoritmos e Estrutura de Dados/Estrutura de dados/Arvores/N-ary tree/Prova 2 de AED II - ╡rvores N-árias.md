---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

**1 - Uma árvore pode se degenerar com o tempo, após muitas inclusões ou exclusões, o que a torna ineficiente no tempo de acesso para a busca. A reconstrução de toda a árvore é um meio de torná-la mais eficiente. Um segundo meio é a adoção de uma árvore autobalanceada, que se reconfigura sempre que ela se torna desbalanceada. Explique uma vantagem e uma desvantagem de cada uma dessas duas formas de manter as árvores balanceadas. A vantagem e a desvantagem deve ser de uma forma sobre a outra forma. Dê um exemplo de árvore autobalanceada.**

Árvores autobalanceadas têm maior custo operacional, pois é necessária a verificação constante da configuração da árvore, pois esse é exatamente seu caráter regenerativo. Considerando esse custo, percebe-se facilmente que não é toda e qualquer situação que se utiliza uma árvore autobalanceada, ficando em função do contexto de uso.

Tendo em vista cada cenário específico, uma das vantagens cruciais da árvore autobalanceada é a previsibilidade do desempenho individual de cada inserção. Como a checagem e a regeneração é constante, teremos uma noção mais precisa de qual será o custo e, com isso, garantir uma distribuição de recursos mais justa. Exemplo disso é o escalonamento de processos do linux e, por lidar com um alto volume de dados, organizados de maneira não estática, essa característica do autobalanceamento pode se tornar essencial para garantir um bom funcionamento - poderíamos chamar de priorização equilibrada. Escalonamento de CPU é um processo que permite que um processo utilize a CPU enquanto outro é colocado em espera, em razão da indisponibilidade de recursos como I/O, assim, otimizando o sistema operacional.

Pensando em um cenário no qual não há um grande volume de operações, a constante verificação torna-se um custo desnecessário, já que a degradação da árvore demoraria mais tempo para se concretizar e, quando isso ocorresse, seria interessante resolver pontualmente ou até mesmo reconstruir a árvore.

-------------------------------------------------------------------------------------------------

**2 - Uma árvore pode ser povoada com muitos dados. Entretanto, não é possível garantir que um valor do centro do intervalo de dados seja recebido primeiro para ser registrado como raiz, ganhando filhos com valores intermediários bem espaçados. Explique sobre a consequência de uma árvore ser povoada com rajadas de valores próximos.**

A principal característica de uma árvore é a forma como seus valores são armazenados. Ao inserir um novo elemento, será realizada uma checagem de valor para determinar qual o branch, à esquerdo ou  direita, o nó filho estará disposto. Dito isso, é fácil perceber que, ao inserir valores próximos em uma árvore, a configuração resultante seria de uma estrutura degradada, visto que os muitos elementos iriam se agrupar em um único ramo, ou ramos próximos. Consequência disso seria uma árvore desbalanceada e ineficiente, perdendo seu propósito inicial.

-------------------------------------------------------------------------------------------------

**3- Uma árvore pode ser muito volumosa. Como consequência, ela pode não ser caber em memória principal e requerer que certos trechos se mantenham em memória secundária. Explique como a localização (memória principal ou secundária) afeta o desempenho da inserção e da busca de dados em uma árvore. Não explique sobre a diferença na velocidade das tecnologias de memória, mas dê alguma outra diferença que também afete o desempenho. Dê um exemplo de mundo real em que o volume de dados normalmente é muito grande, a estrutura normalmente é baseada em árvores, e a estrutura fica armazenada em memória secundária.**


 ---------QUESTIONAVEL - é contígua??????????????

A memória primária não possui características de armazenamento contíguo; em vez disso, os dados são armazenados em células de endereço virtual, cada uma com um endereço específico. Uma das vantagens do armazenamento em memória primária, além de sua alta velocidade, é a realização de operações em tempo constante e a ausência da necessidade de movimentação da memória em função de reajustes. Pensando no armazenamento em memória secundária, sabe-se que sua disposição é feita também de forma linear, porém o acesso a cada elemento não ocorre em tempo constante, visto que não há um endereço específico para cada posição, como ocorre na memória primária.

Um exemplo de armazenamento de uma árvore em memória secundária é a organização de diretórios em um sistema operacional. Organizar todos os arquivos em um sistema operacional é uma tarefa bastante custosa. Dado que a memória primária é geralmente limitada em capacidade, uma abordagem comum é o uso de outras estruturas de dados, como uma lista ou um vetor, que armazenam índices como valores. Esses índices, por sua vez, apontam para uma árvore armazenada na memória secundária. Em tal árvore, cada nó (representando um diretório) é carregado sob demanda, uma vez que carregá-lo integralmente seria um processo demorado.


  
