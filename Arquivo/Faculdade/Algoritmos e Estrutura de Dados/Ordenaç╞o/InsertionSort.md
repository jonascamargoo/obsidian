
O método de inserção (Insertion Sort) é um algoritmo simples de ordenação que constrói uma lista ordenada um elemento de cada vez. Ele percorre a lista original e, a cada iteração, insere o elemento atual em sua posição correta na parte já ordenada da lista.

Aqui está uma descrição passo a passo do algoritmo de ordenação por inserção:

1. O algoritmo começa percorrendo a lista de elementos a serem ordenados, a partir do segundo elemento (índice 1) até o final da lista.
    
2. Em cada iteração, o elemento atual é selecionado para ser inserido na parte ordenada da lista.
    
3. O elemento selecionado é comparado com os elementos na parte ordenada, começando do último elemento até o primeiro.
    
4. Se o elemento atual for menor do que o elemento na posição atual na parte ordenada, os elementos na parte ordenada são deslocados para a direita para abrir espaço para a inserção do elemento atual.
    
5. O elemento atual é então inserido na posição correta na parte ordenada.
    
6. O processo é repetido até que todos os elementos tenham sido percorridos e inseridos corretamente na parte ordenada.
    

O algoritmo de inserção é eficiente para listas pequenas ou parcialmente ordenadas. Ele possui uma complexidade de tempo quadrática (O(n^2)), onde n é o número de elementos na lista. No entanto, o algoritmo pode ter um desempenho melhor do que outros algoritmos de ordenação com complexidade quadrática em certas situações, como quando a lista já está quase ordenada ou possui um pequeno número de elementos.

```
public static void insercao(Item vetor[]) {
    int i, j, n = vetor.length;
    Item aux;
    for (i = 1; i < n; i++) {
        aux = vetor[i];
        j = i - 1;
        while ((j >= 0) && (aux.compara(vetor[j]) < 0)) {
            vetor[j + 1] = vetor[j];
            j--;
        }
        vetor[j + 1] = aux;
    }
}

```

![[Pasted image 20230715182221.png]]

![[Pasted image 20230715182239.png]]