#### O que são?

	- É uma lista linear em que todas as inserções são realizadas em um extremo da lista, e todas as retiradas e, geralmente, os acessos são realizados no outro extremo da lista.

	- O modelo intuitivo de uma fila é o de uma fila de espera em que as pessoas no início da fila são servidas primeiro e as pessoas que chegam entram no fim da fila (FIFO - first in first out)

	- Existe uma ordem linear para filas que é a “ordem de chegada”.

	- São utilizadas quando desejamos processar itens de acordo com a ordem “primeiro-que-chega, primeiro-atendido”.

	- Sistemas operacionais utilizam filas para regular a ordem na qual tarefas devem receber processamento e recursos devem ser alocados a processos.

#### Conjunto de operações:

	-  Criar uma fila vazia.
	- Enfileirar o item x no final da fila.
	- Desenfileirar. Essa função retorna o item x no início da fila e o retira da fila.
	- Verificar se a fila está vazia. Essa função retorna true se a fila está vazia; do contrário, retorna false.


#### Implementação por meio de arranjos

	- Os itens são armazenados em posições contíguas de memória;
	- A operação Enfileira faz a parte de trás (fim) da fila expandir-se;
	- A operação Desenfileira faz a parte da frente (inicio) da fila contrair-se;
	- A fila tende a caminhar pela memória do computador, ocupando espaço na parte de trás (fim) e descartando espaço na parte da frente (inicio);
	- Com poucas inserções e retiradas, a fila vai ao encontro do limite do espaço da memória alocado para ela;
	- Solução: imaginar o array como um círculo. A primeira posição segue a última;

![[Pasted image 20230618110051.png]]


	- A fila se encontra em posições contíguas de memória, em alguma posição do círculo, delimitada pelos apontadores inicio e fim. (inicio indica a posição do primeiro elemento, fim a primeira posição vazia);
	- Para enfileirar, basta mover o apontador fim uma posição no sentido horário;
	- Para desenfileirar, basta mover o apontador inicio uma posição no sentido horário.
	- O tamanho máximo do arranjo circular é definido pela constante maxTam;
	- Os outros campos da classe Fila contêm referências para o inicio e o fim da fila.
	- Nos casos de fila cheia e fila vazia, os apontadores inicio e fim apontam para a mesma posição do círculo.
	- Uma saída para distinguir as duas situações é deixar uma posição vazia no arranjo.
	- Neste caso, a fila está cheia quando fim+1 for igual a inicio.
	- A implementação utiliza aritmética modular nos procedimentos enfileira e desenfileira (% do Java).

```
public class FilaE<T> {
	private T item[];  // Array to store queue elements
	private int inicio, fim;  // Pointers to track the start and end of the queue

	public FilaE(int maxTam) {  // Constructor to create an empty queue
	    item = (T[]) new Object[maxTam];  // Create a new array of type T
	    inicio = 0;  // Set the start pointer to 0
	    fim = inicio;  // Set the end pointer to the start pointer
	}
	
	public void enfileira(T item) throws Exception {
	    if (item == null)
	        throw new NullPointerException();
	
	    if ((fim + 1) % this.item.length == inicio)
	        throw new Exception("Erro: A fila esta cheia");
	
	    this.item[fim] = item;  // Add the item to the end of the queue
	    fim = (fim + 1) % this.item.length; // Update the end pointer (wrap   around if necessary)
	}

	public T desenfileira() throws Exception {
	    if (isVazia())
	        throw new Exception("Erro: A fila esta vazia");
	    
	    T item = this.item[inicio];
	    inicio = (inicio + 1) % this.item.length;
	    return item;
	}

	public boolean isVazia() {
	    return (inicio == fim);
	}



}
```


#### Implementação por meio de estruturas auto-referenciadas

	- Há uma célula sentinela para facilitar a implementação das operações enfileira e desenfileira quando a fila está vazia.
	- Quando a fila está vazia, as referências inicio e fim referenciam para a célula sentinela.
	- Para enfileirar um novo item, basta criar uma célula nova, ligá-la após a célula que contém Xn e colocar nela o novo item.
	- Para desenfileirar o item X1 , basta desligar a célula sentinela da lista e a célula que contém X1 passa a ser a célula sentinela.

![[Pasted image 20230618111214.png]]

	- A fila é implementada por meio de células.
	- Cada célula contém um item da fila e uma referência para outra célula.
	- A classe Fila contém uma referência para a inicio da fila (célula sentinela) e uma referência para o fim da fila.


```
public class FilaD<T> {
	private Celula inicio;
	private Celula fim;
	private int tamanho;
	
	public class Celula {
	    T item;
	    Celula prox;
    
    public Celula(T item) {
        this.item = item;
    }
    
    public Celula() {}
	
	public FilaD() {
	    inicio = new Celula();  // head or sentinel node
	    fim = inicio;
	    tamanho = 0;
	}
	
	public void enfileira(T item) {
    if (item == null)
        throw new NullPointerException();
    else {
        fim.prox = new Celula(item);
        fim = fim.prox;
        tamanho++;
    }
}

	public T desenfileira() throws Exception {
	    if (isVazia())
	        throw new Exception("Erro: Fila vazia!");
	    else {
	        inicio = inicio.prox;
	        tamanho--;
	        return inicio.item;
	    }
	}
	
	public boolean isVazia() {
	    return (inicio == fim);
	}

}
```