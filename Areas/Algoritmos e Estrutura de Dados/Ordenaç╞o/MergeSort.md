O Merge Sort é um algoritmo de ordenação eficiente e estável que utiliza a estratégia "dividir para conquistar". Ele divide a lista em partes menores, ordena cada parte separadamente e, em seguida, combina as partes ordenadas para obter a lista final ordenada. Esse processo de divisão e combinação é repetido recursivamente até que a lista esteja completamente ordenada.

Aqui está uma descrição passo a passo do algoritmo de ordenação Merge Sort:

1. O Merge Sort começa dividindo a lista original em duas partes iguais.
    
2. Em seguida, aplica o Merge Sort recursivamente em cada uma das partes, dividindo-as novamente em partes menores até que cada parte contenha apenas um elemento.
    
3. Depois de dividir as partes em elementos individuais, começa o processo de combinação. Duas partes adjacentes são combinadas e seus elementos são comparados.
    
4. Durante a combinação, os elementos são inseridos em uma nova lista de forma ordenada. Os elementos são comparados e movidos para a nova lista de acordo com sua ordem.
    
5. Esse processo de combinação continua até que todas as partes tenham sido combinadas em uma única lista ordenada.
    

O Merge Sort possui as seguintes características:

- Eficiência: O Merge Sort tem uma complexidade de tempo média e pior caso de O(n log n), onde n é o número de elementos na lista. Isso torna o Merge Sort um dos algoritmos de ordenação mais eficientes em termos de tempo de execução.
    
- Estabilidade: O Merge Sort é um algoritmo de ordenação estável, o que significa que ele preserva a ordem relativa dos elementos com chaves iguais. Isso é importante quando é necessário manter a ordem original de elementos com valores repetidos.
    
- Necessidade de memória adicional: O Merge Sort requer espaço adicional na memória para armazenar os elementos temporariamente durante o processo de combinação. Isso é feito através de um array auxiliar que é utilizado para mesclar as partes ordenadas.
    
- Recursividade: O Merge Sort é implementado de forma recursiva, dividindo a lista original em partes menores. A recursão permite que o algoritmo seja aplicado em cada sublista de forma independente.
    

O Merge Sort é amplamente utilizado devido à sua eficiência e estabilidade. Ele é particularmente útil para ordenar listas de tamanho médio a grande, onde o desempenho e a estabilidade são fatores importantes. No entanto, em alguns casos, o uso de memória adicional pode ser uma desvantagem, especialmente quando se lida com conjuntos de dados muito grandes.

Em resumo, o Merge Sort é um algoritmo de ordenação eficiente que divide a lista original em partes menores, ordena cada parte separadamente e, em seguida, combina as partes ordenadas para obter a lista final ordenada. Ele possui uma complexidade de tempo média de O(n log n) e é estável. O Merge Sort é uma escolha comum quando é necessário um algoritmo de ordenação eficiente e estável para listas de tamanho médio a grande.

```
void mergesort(Item[] a, Item[] aux) {
    merge(a, aux, 0, a.length - 1);
}

void merge(Item[] a, Item[] aux, int inicio, int fim) {
    int meio;
    if (inicio != fim) {
        meio = (inicio + fim) / 2;
        merge(a, aux, inicio, meio);
        merge(a, aux, meio + 1, fim);
        intercala(a, aux, inicio, meio, fim);
    }
}

void intercala(Item[] a, Item[] aux, int inicio, int meio, int fim) {
    // Copiando o trecho do vetor que vai ser ordenado
    for (int i = inicio; i <= fim; i++)
        aux[i] = a[i];

    int i = inicio, k = inicio, j = meio + 1;
    // Junção das listas ordenadas
    while (i <= meio && j <= fim) {
        if (aux[i].compara(aux[j]) < 0)
            a[k++] = aux[i++];
        else
            a[k++] = aux[j++];
    }
    // Acrescenta itens que não foram usados na junção
    while (i <= meio)
        a[k++] = aux[i++];
    while (j <= fim)
        a[k++] = aux[j++];
}
```

### Análise de complexidade


![[Pasted image 20230715211419.png]]
![[Pasted image 20230715211440.png]]