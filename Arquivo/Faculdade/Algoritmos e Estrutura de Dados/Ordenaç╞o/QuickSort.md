---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

O Quick Sort é um algoritmo de ordenação eficiente e amplamente utilizado que também utiliza a estratégia "dividir para conquistar". Ele seleciona um elemento como pivô e rearranja os elementos em torno do pivô, de forma que os elementos menores fiquem à esquerda e os elementos maiores fiquem à direita. Em seguida, o Quick Sort é aplicado recursivamente nas duas partes resultantes do pivô até que toda a lista esteja ordenada.

Aqui está uma descrição passo a passo do algoritmo de ordenação Quick Sort:

1. O Quick Sort seleciona um elemento da lista como pivô. Geralmente, o pivô é escolhido como o último elemento da lista, mas outras estratégias de seleção de pivô podem ser usadas.
    
2. Os elementos da lista são rearranjados em torno do pivô de forma que os elementos menores que o pivô estejam à esquerda e os elementos maiores estejam à direita. Isso é conhecido como a etapa de particionamento.
    
3. Após o particionamento, o pivô ocupa sua posição final na lista ordenada. Os elementos menores que o pivô estão à esquerda dele e os elementos maiores estão à direita dele.
    
4. O Quick Sort é aplicado recursivamente nas duas partes resultantes do pivô (à esquerda e à direita), repetindo o processo de particionamento até que cada parte tenha apenas um elemento.
    
5. No final do processo recursivo, a lista estará completamente ordenada.
    

O Quick Sort possui as seguintes características:

- Eficiência: Em média, o Quick Sort possui uma complexidade de tempo de O(n log n), onde n é o número de elementos na lista. No entanto, em seu pior caso, quando a escolha do pivô não é adequada, a complexidade pode chegar a O(n^2). No entanto, com uma escolha adequada do pivô e particionamento equilibrado, o Quick Sort é um dos algoritmos de ordenação mais rápidos.
    
- In-place: O Quick Sort é um algoritmo in-place, o que significa que ele não requer espaço adicional na memória além da lista original. Ele rearranja os elementos na própria lista de entrada.
    
- Não é estável: O Quick Sort não preserva a ordem relativa dos elementos com chaves iguais. Durante o processo de particionamento e trocas, a ordem original dos elementos pode ser alterada.
    

Aqui está uma implementação do Quick Sort em Java:

```
public static void quickSort(int[] vetor, int inicio, int fim) {
    if (inicio < fim) {
        int posicaoPivo = particionar(vetor, inicio, fim);
        quickSort(vetor, inicio, posicaoPivo - 1);
        quickSort(vetor, posicaoPivo + 1, fim);
    }
}

public static int particionar(int[] vetor, int inicio, int fim) {
    int pivo = vetor[fim];
    int i = inicio - 1;
    
    for (int j = inicio; j < fim; j++) {
        if (vetor[j] < pivo) {
            i++;
            trocar(vetor, i, j);
        }
    }
    
    trocar(vetor, i + 1, fim);
    return i + 1;
}

public static void trocar(int[] vetor, int i, int j) {
    int temp = vetor[i];
    vetor[i] = vetor[j];
    vetor[j] = temp;
}

```