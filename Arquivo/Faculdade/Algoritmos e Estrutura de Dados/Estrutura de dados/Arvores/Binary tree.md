---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

## Definição

1. **Árvore Binária:** Cada nó na árvore binária de busca tem, no máximo, dois filhos: um filho à esquerda e um filho à direita.
    
2. **Estrutura de Busca:** A principal característica da Árvore Binária de Busca é sua estrutura de busca eficiente. Os nós são organizados de forma que os valores dos nós à esquerda são menores que o valor do nó pai, e os valores dos nós à direita são maiores.
    
3. **Profundidade Média:** Como mencionado, a profundidade média dos nós em uma Árvore Binária de Busca costuma ser menor do que n, o que a torna uma estrutura de dados eficiente para operações de busca, inserção e exclusão.
    
4. **Complexidade de Tempo:** As operações de busca, inserção e exclusão em uma Árvore Binária de Busca têm complexidade de tempo médio de 𝑂(log 𝑛), onde 𝑛 é o número de nós na árvore. No entanto, em casos extremos, a árvore pode degenerar em uma [[Lineares vs Encadeadas|lista]], resultando em uma complexidade de tempo de 𝑂(𝑛).
    

## Implementação
#### Node

Primeiramente, a implementação do nó

```java
private static class BinaryNode<T> {
    // Atributos da classe
    T element;              // Elemento armazenado no nó
    BinaryNode<T> left;     // Nó à esquerda
    BinaryNode<T> right;    // Nó à direita

    // Construtor para criar um nó com elemento
    BinaryNode(T element) {
        this.element = element;
        this.left = null;
        this.right = null;
    }

    // Construtor para criar um nó com elemento, nó à esquerda e nó à direita
    BinaryNode(T element, BinaryNode<T> left, BinaryNode<T> right) {
        this.element = element;
        this.left = left;
        this.right = right;
    }
}

```

### Contains

Método contains. Este método `contains` verifica se um elemento `x` está presente na árvore binária representada pelo nó `tree`. Ele faz isso comparando o elemento atual do nó com o elemento `x` e navegando para a subárvore à esquerda ou à direita com base na comparação. Se o elemento for encontrado na árvore, o método retorna `true`. Caso contrário, ele retorna `false`.


```java
private boolean contains(T x, BinaryNode<T> tree) {
    // Verifica se a árvore está vazia (nulo)
    if (tree == null) {
        return false; // O elemento não foi encontrado na árvore
    }

    // Compara o elemento a ser procurado com o elemento atual da árvore
    int compareResult = x.compareTo(tree.element);

    // Se o elemento for menor, continue a busca na subárvore à esquerda
    if (compareResult < 0) {
        return contains(x, tree.left);
    }
    // Se o elemento for maior, continue a busca na subárvore à direita
    else if (compareResult > 0) {
        return contains(x, tree.right);
    }
    // Se os elementos forem iguais, o elemento foi encontrado na árvore
    else {
        return true;
    }
}

```

### Máximo e mínimo

Os métodos findMin e findMax retornam uma referência para o nó contando o menor e o maior elemento da árvore, respectivamente. Para implementar o findMin, deve-se começar pela raiz e ir o mais à esquerda possível. O ponto de parada é o menor elemento. Enquanto o findMax é o mesmo, porém em direção contrária. Esse método ilustra, a principal vantagem de uma árvore de busca binária - fácil ordenação. A implementação das rotinas de forma recursiva e não recursiva:

```java
// recursivo
private BinaryNode<T> findMin(BinaryNode<T> tree) {
    // Verifique se a árvore está vazia
    if (tree == null) {
        return null;
    }
    
    // Se não houver um nó à esquerda, este é o valor mínimo
    if (tree.left == null) {
        return tree;
    }
    
    // Continue a busca na subárvore à esquerda recursivamente
    return findMin(tree.left);
}

// nao recursivo
private BinaryNode<T> findMax(BinaryNode<T> tree) {
    // Verifique se a árvore está vazia
    if (tree == null) {
        return null;
    }
    
    // Continue à direita até encontrar o valor máximo
    while (tree.right != null) {
        tree = tree.right;
    }
    
    return tree;
}

```

### Inserção

Para inserir X dentro da árvore, deve-se analisar primeiramente se o nó X já está inserido. Caso não esteja, o nó é inserido na última posição, mantendo a propriedade em que os valores mais altos ficam à direita e os menores à esquerda. Para inserir de maneira desordenada, basta não realizar a comparação entre valores:

```java
// ordenada
private TreeNode<T> insertSorted(T node, TreeNode<T> tree) {
    // Se a árvore estiver vazia, insira o novo nó como raiz
    if (tree == null) {
        return new TreeNode<T>(node, null, null);
    }
    
    int compareResult = node.compareTo(tree.element);
    
    // Insira à esquerda se o novo nó for menor
    if (compareResult < 0) {
        tree.left = insertSorted(node, tree.left);
    }
    // Insira à direita se o novo nó for maior
    else if (compareResult > 0) {
        tree.right = insertSorted(node, tree.right);
    }
    // Ignorar duplicatas (nós com o mesmo valor)
    
    return tree;
}

// desordenada
private TreeNode<T> insert(T node, TreeNode<T> tree) {
    // Se a árvore estiver vazia, insira o novo nó como raiz
    if (tree == null) {
        return new TreeNode<T>(node, null, null);
    }
    
    // Insira sempre à esquerda (desordenada pela direita)
    tree.left = insert(node, tree.left);
    
    return tree;
}

```

### Exclusão

Em relação à remoção de elementos em árvores de busca binária, deve-se considerar alguns fatores a mais. Primeiramente, caso o nó seja uma folha, ele pode ser deletado imediatamente. Se tiver um filho, só poderá ser removido após o seu nó pai ser ajustado para ignorá-lo. O pior caso consiste em um tentar eliminar um nó que possui dois filhos. A estratégia para esse caso é substituir o valor desse nó pelo menor valor da árvore à direita e recursivamente, deletar o nó (agora vazio). Pelo fato de o menor nó da sub árvore direita não poder ter um filho à esquerda, a segunda remoção é mais fácil. A implementação do método fica da seguinte forma:

```java
private BinaryNode<T> remove(T x, BinaryNode<T> tree) {
    // Caso base: árvore vazia, não há nada para remover
    if (tree == null) {
        return tree;
    }
    
    int compareResult = x.compareTo(tree.element);
    
    // Se o valor a ser removido for menor, continue à esquerda
    if (compareResult < 0) {
        tree.left = remove(x, tree.left);
    }
    // Se o valor a ser removido for maior, continue à direita
    else if (compareResult > 0) {
        tree.right = remove(x, tree.right);
    }
    // Encontrou o nó a ser removido
    else {
        // Caso 1: Nó com nenhum ou um filho
        if (tree.left == null) {
            return tree.right;
        } else if (tree.right == null) {
            return tree.left;
        }
        // Caso 2: Nó com dois filhos
        tree.element = findMin(tree.right).element; // Encontra o sucessor (valor mínimo à direita)
        tree.right = remove(tree.element, tree.right); // Remove o sucessor
    }
    
    return tree;
}

```

### Impressão por iteração

O algoritmo a ser implementado é chamado Morris Traversal. A travessia de Morris (InOrder) é um algoritmo de travessia de árvore que não emprega o uso de recursão ou pilha. Nesta travessia, os links são criados como sucessores e os nós são impressos usando esses links. Por fim, as alterações são revertidas para restaurar a árvore original. O algoritmo possui complexidade de tempo linear e funciona da seguinte maneira: • Inicializa a raiz como nó atual 𝑐𝑢𝑟𝑟 • Enquanto 𝑐𝑢𝑟𝑟 não for nulo, checa se 𝑐𝑢𝑟𝑟 possui um filho a esquerda • Se 𝑐𝑢𝑟𝑟 não tiver um filho à esquerda, imprime 𝑐𝑢𝑟𝑟 e atualiza a sub árvore esquerda • Caso contrário, 𝑐𝑢𝑟𝑟 recebe o filho à direita do nó mais à direita na árvore esquerda atual • Atualiza 𝑐𝑢𝑟𝑟 para o nó esquerdo

```java
private void inOrderMorris() {
    BinaryNode<T> cur = root;
    while (cur != null) {
        if (cur.left == null) {
            // Se não houver filho à esquerda, visite o nó atual e vá para a direita
            System.out.print(cur.element + " ");
            cur = cur.right;
        } else {
            // Se houver um filho à esquerda, encontre o predecessor
            BinaryNode<T> temp = cur.left;
            while (temp.right != null && temp.right != cur) {
                temp = temp.right;
            }

            if (temp.right == null) {
                // Se o predecessor não tiver um link para o nó atual, crie um link
                temp.right = cur;
                cur = cur.left;
            } else {
                // Se o predecessor já tiver um link para o nó atual, visite o nó atual e remova o link
                temp.right = null;
                System.out.print(cur.element + " ");
                cur = cur.right;
            }
        }
    }
}

```

Este código implementa um percurso em ordem utilizando o algoritmo de Morris, que permite fazer a travessia da árvore binária sem usar uma pilha de chamadas recursivas e com espaço adicional constante. O algoritmo usa ponteiros adicionais para estabelecer conexões temporárias na árvore, permitindo que você vá para a esquerda, visite um nó e depois vá para a direita, mantendo o percurso em ordem correto. Os comentários explicam o funcionamento de cada parte do código.

### Considerações

**Árvore Binária de Busca (BST):** Uma Árvore Binária de Busca é uma estrutura de dados especial em que cada nó possui dois filhos, sendo que os valores dos nós na subárvore esquerda são menores que o valor do nó pai, e os valores na subárvore direita são maiores. Essa organização permite uma ordenação eficiente dos elementos.

**Complexidade Média de Profundidade:** Em uma Árvore Binária de Busca, o valor médio de profundidade é 𝑂(log 𝑛), onde 𝑛 representa o número de elementos na árvore. Isso se deve à natureza da busca binária, que reduz o escopo pela metade a cada nível da árvore.

**Complexidade Média das Operações:** Para a maioria das operações em uma Árvore Binária de Busca, a complexidade é 𝑂(𝑑), em que 𝑑 é a profundidade do nó que contém o item sendo acessado. No entanto, é importante destacar que, no pior caso, a profundidade pode ser 𝑂(𝑛), o que torna a operação menos eficiente.

**Comparação com Estruturas Lineares:** Comparando com outras estruturas de dados, como vetores e listas encadeadas, uma Árvore Binária de Busca oferece vantagens em diferentes operações. Ela é eficaz na busca de elementos, com complexidade média de 𝑂(log 𝑛), mas pode ser menos eficiente do que um vetor em termos de acesso direto a elementos. Além disso, a inserção é mais rápida do que em algumas estruturas, como listas encadeadas, mas menos eficiente que a de vetores.

**Escolha de Estruturas Hierárquicas:** A escolha entre diferentes estruturas de dados, incluindo árvores, depende das necessidades específicas de um problema. Árvores, com sua estrutura hierárquica, podem ser ideais para certos casos, mas é importante avaliar as características de cada estrutura em relação aos requisitos do problema para fazer a escolha mais apropriada.