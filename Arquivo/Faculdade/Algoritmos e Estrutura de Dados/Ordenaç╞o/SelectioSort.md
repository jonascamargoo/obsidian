---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

	O Selection Sort é um algoritmo de ordenação simples que divide a lista em duas partes: uma parte ordenada e uma parte não ordenada. A cada iteração, o algoritmo seleciona o elemento mínimo da parte não ordenada e o move para a posição correta na parte ordenada.


```
public static void selectionSort(int vetor[]) {
    int n = vetor.length;
    for (int i = 0; i < n - 1; i++) {
        int indiceMinimo = i;
        for (int j = i + 1; j < n; j++) {
            if (vetor[j] < vetor[indiceMinimo]) {
                indiceMinimo = j;
            }
        }
        // Troca o elemento mínimo com o primeiro elemento não ordenado
        int temp = vetor[indiceMinimo];
        vetor[indiceMinimo] = vetor[i];
        vetor[i] = temp;
    }
}

```

![[Pasted image 20230715181403.png]]

#### Vantagens:
* Custo linear no tamanho da entrada para o número de
movimentos de registros.
* É o algoritmo a ser utilizado para arquivos com registros
muito grandes.
* É muito interessante para arquivos pequenos.

#### Desvantagens:
* Não adaptável
* Não importa se o arquivo está parcialmente ordenado, pois o custo continua quadrático.
- O algoritmo não é estável.