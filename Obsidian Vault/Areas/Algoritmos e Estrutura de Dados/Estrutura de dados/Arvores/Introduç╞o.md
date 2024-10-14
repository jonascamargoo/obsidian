## Definição inicial de árvores

Árvores, sendo um tipo abstrato de dados, podem ser definidas de várias maneiras. Uma definição comum é considerar uma árvore como uma coleção hierárquica de nós conectados por arestas. Se a coleção não estiver vazia, ela inclui um nó distinto chamado raiz, além de zero ou mais subárvores não vazias, denotadas como 𝑇, 𝑇2, ..., 𝑇𝑘. Cada raiz dessas subárvores está ligada à raiz principal por uma aresta. Os termos "raiz" e "subárvore" são derivados do inglês "root" e "tree", respectivamente. As raízes das subárvores são chamadas de filhas da raiz principal, enquanto a raiz principal é o pai de cada uma das subárvores.

Em uma árvore, cada nó pode ter vários filhos, inclusive nenhum. Se um nó não tiver filhos, é chamado de folha. Os nós que compartilham o mesmo pai são considerados irmãos. Além disso, a analogia de netos e avôs também pode ser aplicada.

O caminho de um nó 𝑛1 até 𝑛𝑘 é uma sequência de nós onde cada nó 𝑛𝑖 é o pai do próximo nó 𝑛𝑖+1, para 1 ≤ 𝑖 < 𝑘. O comprimento desse caminho é igual ao número de arestas, que é 𝑘−1. É importante notar que há sempre um caminho único da raiz até cada nó na árvore. A profundidade de um nó é determinada pelo caminho único que o conecta à raiz, onde a raiz está na profundidade zero.

A altura de um nó é o comprimento do caminho mais longo do nó até uma folha. Cada folha tem uma altura de zero. A altura da árvore é igual à altura de sua raiz. A profundidade de uma árvore é sempre igual à sua altura, que, por sua vez, é equivalente à profundidade de sua folha mais profunda.

Finalmente, se houver um caminho entre 𝑛1 e 𝑛2, 𝑛1 é considerado ancestral de 𝑛2, e, por sua vez, 𝑛2 é descendente de 𝑛1. Se 𝑛1 for diferente de 𝑛2, 𝑛1 é o ancestral direto de 𝑛2, enquanto 𝑛2 é o descendente direto de 𝑛1.

