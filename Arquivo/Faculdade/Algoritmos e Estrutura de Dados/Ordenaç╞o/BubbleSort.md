---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

## Ideia
* Passa no arquivo e troca elementos adjacentes que estão fora de ordem
* Repete esse processo até que o arquivo esteja ordenado

## Algoritmo
* Compara dois elementos adjacentes e troca de posição se estiverem fora de ordem
* Quando o maior elemento do vetor for encontrado, ele será trocado até ocupar a última posição
* Na segunda passada, o segundo maior será movido para a penúltima posição do vetor, e assim sucessivamente


```
public static void bolha(Item vetor[]) {
    int n = vetor.length;
    Item aux;
    for (int i = 0; i < n - 1; i++) {
        for (int j = 1; j < n - i; j++) {
            // if (v[j] < v[j-1])
            if (vetor[j].compara(vetor[j - 1]) < 0) {
                aux = vetor[j];
                vetor[j] = vetor[j - 1];
                vetor[j - 1] = aux;
            }
        }
    }
}

```


![[Pasted image 20230715175236.png]]

#### Vantagens:

* Algoritmo simples
* Algoritmo estável
* Uso constante de memória
* O fato de o arquivo já está (quase) ordenado minimiza as trocas

#### Desvantagens:

* Muitas trocas de itens
* Não adaptável.