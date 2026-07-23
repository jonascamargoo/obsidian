---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

## Definição

Em computação, listas são estruturas de dados que organizam elementos de forma sequencial, permitindo o armazenamento, acesso e manipulação de informações. As listas podem ser usadas para representar uma coleção ordenada de itens, onde cada item pode conter dados ou referências a outros elementos.
## Listas lineares x listas encadeadas

### Lista linear

* **Armazenamento Contíguo:** Em uma lista linear, como um array, os elementos são armazenados de forma contígua na memória. Cada elemento ocupa uma posição de memória consecutiva;
* **Acesso Direto por Índice:** O acesso aos elementos é feito diretamente por meio de índices. Isso significa que você pode acessar qualquer elemento da lista em tempo constante, pois basta calcular o endereço base e adicionar um deslocamento multiplicado pelo tamanho dos elementos;
* **Tamanho Fixo ou Dinâmico:** O tamanho de uma lista linear pode ser fixo (em arrays) ou dinâmico (em algumas implementações de listas dinâmicas, como ArrayList em Java).

### Lista Encadeada (lista ligada)

* **Armazenamento Não Contíguo:** Em listas encadeadas, os elementos não são armazenados de maneira contígua na memória. Cada elemento contém um ponteiro (referência) para o próximo elemento na sequência;
* **Acesso Sequencial:** Para acessar um elemento em uma lista encadeada, você precisa percorrer sequencialmente a lista a partir do início (ou do final, dependendo da implementação). O acesso direto por índice não é possível sem percorrer a lista;
* **Tamanho Dinâmico:** Listas encadeadas podem facilmente crescer ou diminuir em tamanho, pois os elementos podem ser adicionados ou removidos sem a necessidade de realocação de memória;
* **Tipos de Listas Encadeadas:** Existem diferentes tipos de listas encadeadas, como simplesmente encadeadas (cada elemento aponta para o próximo), duplamente encadeadas (cada elemento aponta para o próximo e o anterior), e circularmente encadeadas (a última aponta para a primeira).


| Cabeçalho 1 | Linear | Encadeada |
| ---- | ---- | ---- |
| add() | O(n) ou O(1) | O(1) |
| get() | O(1) | O(n) |
| remove(element) | O(n) | O(n) |
| remove(i) | O(n) | O(n) |
| remove(0) | O(n) | O(1) |
| remove(last) | O(1) | O(1) |
| indexOf() | O(n) | O(n) |
| contains() | O(o) | O(n) |

OBS: em add(), se vai ser O(n) ou O(1), explico [[Lista Lineares|aqui]], em "tamanho dinâmico". Além disso, estou considerando a lista duplamente encadeada. Além disso, operações de remoção em listas lineares são O(n) pois precisam fazer copias dos subsequentes (arredar).
## Dicas:

Se tiver de adicionar e remover , use encadeada. Se tiver tamanho fixo, use linear. Se tiver de acessar elementos de forma aleatória (em qualquer posição), use linear, pois é indexado.
