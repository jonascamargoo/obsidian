
## Características

#### Arranjo sequencial
	A ordenação envolve organizar os elementos em uma sequência linear, geralmente em uma lista, vetor ou matriz, onde cada elemento tem uma posição definida em relação aos demais.

####  Critério de ordenação
	A ordenação é baseada em um critério específico, que determina a ordem dos elementos. Esse critério pode ser simples, como a ordem numérica crescente ou decrescente, ou mais complexo, levando em consideração múltiplos atributos ou regras de comparação personalizadas.

#### Estabilidade
	A estabilidade se refere à preservação da ordem relativa dos elementos com chaves iguais durante o processo de ordenação. Em uma ordenação estável, se dois elementos têm chaves iguais, a ordem original entre eles é mantida no resultado ordenado;

#### Adaptabilidade
	Um método é adaptável quando a sequencia de operações realizadas depende da entrada. Um método que sempre realiza as mesmas operações, independente da entrada, é não adaptável.

#### Ordenação interna

	A ordenação interna ocorre quando todos os dados a serem ordenados cabem na memória principal (RAM) do computador. Isso significa que os dados estão acessíveis de forma direta e rápida durante todo o processo de ordenação. Os algoritmos de ordenação interna são projetados para trabalhar com os dados presentes na memória principal e realizam as operações de comparação e troca de elementos nesse espaço. Os algoritmos de ordenação interna, como o Quicksort, Mergesort, Heapsort, Insertion Sort e Selection Sort, são eficientes quando todos os dados estão disponíveis na memória principal. Eles podem ser implementados de maneira simples e tendem a ter uma alta velocidade de execução, dependendo das características dos dados e do algoritmo escolhido.


#### Ordenação externa

	A ordenação externa ocorre quando os dados a serem ordenados são maiores do que a capacidade da memória principal. Isso geralmente acontece quando há uma quantidade muito grande de dados ou quando o tamanho dos dados individuais é grande. Nesses casos, os dados são armazenados em dispositivos de armazenamento secundário, como discos rígidos, SSDs ou fitas magnéticas.
	
	Durante a ordenação externa, apenas uma parte dos dados é lida da memória secundária para a memória principal, onde ocorrem as operações de comparação e troca. Essa parte dos dados é conhecida como bloco ou página de entrada/saída. À medida que a ordenação progride, os blocos são lidos e gravados repetidamente na memória secundária para a realização das operações necessárias. Esse processo de leitura/gravação de blocos é chamado de mesclagem (merge) e é uma das principais técnicas utilizadas na ordenação externa.


## Métodos de ordenação

Métodos simples: Bolha (BubbleSort), Seleção (SelectSort), Inserção (InsertSort)

Métodos Eficientes: Shellsort, Quicksort, Heapsort

![[Pasted image 20230715173120.png]]


## Ordenação simples x ordenação eficiente

#### Métodos Simples:

Os métodos de ordenação simples são algoritmos de ordenação adequados para lidar com entradas menores. Eles são fáceis de entender e implementar, resultando em programas pequenos e compactos. No entanto, esses métodos possuem uma complexidade de tempo quadrática (O(n^2)), o que significa que eles requerem um número de comparações proporcional ao quadrado do tamanho da entrada.

Um exemplo de método de ordenação simples é o Bubble Sort, que compara e troca elementos adjacentes até que a lista esteja completamente ordenada. Outros métodos simples incluem o Selection Sort, que seleciona o menor elemento e o coloca na posição correta a cada iteração, e o Insertion Sort, que constrói uma lista ordenada um elemento de cada vez.

Esses métodos podem ser eficientes para listas pequenas ou parcialmente ordenadas, onde a simplicidade de implementação e a economia de recursos são mais importantes do que a velocidade de execução. No entanto, à medida que o tamanho da entrada aumenta, esses métodos se tornam menos eficientes em comparação com métodos mais sofisticados.

#### Métodos Eficientes:

Os métodos de ordenação eficientes são projetados para lidar com entradas maiores e têm um desempenho melhor em termos de tempo de execução. Esses métodos possuem uma complexidade de tempo média de O(n log n), onde n é o tamanho da entrada. Isso significa que eles requerem um número de comparações proporcional ao produto do tamanho da entrada pelo logaritmo desse tamanho.

Alguns exemplos de métodos de ordenação eficientes são o Merge Sort, que divide a lista em partes menores, ordena-as separadamente e, em seguida, mescla as partes ordenadas, e o Quick Sort, que seleciona um elemento pivô e particiona a lista em elementos menores e maiores em relação a ele, repetindo o processo nas duas partições.

Esses métodos eficientes usam técnicas avançadas, como a divisão e conquista, para reduzir o número de comparações necessárias e acelerar o processo de ordenação. Embora eles possam ser mais complexos em termos de detalhes de implementação e exigir algoritmos mais elaborados, eles oferecem uma melhoria significativa no desempenho para entradas maiores.