---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

#### O que são?

- LIFO (last in first out)
- É uma lista linear em que todas as inserções, retiradas e, geralmente, todos os acessos são feitos em apenas um extremo da lista.
- Os itens são colocados um sobre o outro. O item inserido mais recentemente está no topo e o inserido menos recentemente no fundo.
- O modelo intuitivo é o de um monte de pratos em uma prateleira, sendo conveniente retirar ou adicionar pratos na parte superior.
- Esta imagem está frequentemente associada com a teoria de autômato, na qual o topo de uma pilha é considerado como o receptáculo de uma cabeça de leitura/gravação que pode empilhar e desempilhar itens da pilha.

#### aplicações

- É ideal para processamento de estruturas aninhadas de profundidade imprevisível.
- Uma pilha contém uma sequência de obrigações adiadas. A ordem de remoção garante que as estruturas mais internas serão processadas antesdas mais externas.

- Aplicações em estruturas aninhadas:
	- Quando é necessário caminhar em um conjunto de dados e guardar uma lista de coisas a fazer posteriormente.
	- O controle de sequências de chamadas de subprogramas.
	-  A sintaxe de expressões aritméticas.
- As pilhas ocorrem em estruturas de natureza recursiva (como árvores). Elas são utilizadas para implementar a recursividade.

### TAD Pilha

- Conjunto de operações:
	- Cria uma pilha Vazia.
	- Verifica se a pista está vazia. Retorna true se a pilha está vazia; caso contrário, retorna false.
	- Empilhar o item x no topo da pilha.
	- Desempilhar o item x no topo da pilha, retirando-o da pilha.
	- Verificar o tamanho atual da pilha.


- Existem várias opções de estruturas de dados que podem ser usadas para representar pilhas:
	- Arranjos
	- Apontadores
	

#### Estrutura de dados de pilhas através de arranjos
- Os itens da pilha são armazenados em posições contíguas de memória;
- Como as inserções e as retiradas ocorrem no topo da pilha, um campo chamado Topo é utilizado para controlar a posição do item no topo da pilha;

![[Pasted image 20230616120021.png]]

#### Estrutura de dados de pilhas através de arranjos

- Os itens são armazenados em um arranjo de tamanho suficiente para conter a pilha.
- O outro campo do mesmo registro contém uma referência para o item no topo da pilha.
- A constante maxTam define o tamanho máximo permitido para a pilha.

```
public class Pilha<T> {
	private T item[];
	private int topo;

	// Operações
	public Pilha(int maxTam) { // Cria uma Pilha vazia
		item = (T[]) new Object[maxTam];
		topo = 0;
	}

	public void empilha(T item) throws RuntimeException {
		if (item == null)
			throw new NullPointerException();
		if (topo == this.item.length)
			throw new RuntimeException("Erro: A pilha esta cheia");
		else
			this.item[topo++] = item;
	}

	public T desempilha() throws RuntimeException {
		if (vazia())
			throw new RuntimeException("Erro: A pilha esta vazia");
		return item[--topo];
	}

	public boolean vazia() {
		return (topo == 0);
	}

	public int tamanho() {
		return topo;
	}
}
```


#### Implementação de Pilhas por meio de Estruturas Auto-Referenciadas

- Ao contrário da implementação de listas lineares por meio de estruturas auto referenciadas, na pilha não há necessidade de manter uma célula sentinela no topo.

- Para desempilhar o item Xn basta desligar a célula sentinela da lista e a célula que contém X(n-1) passa a ser a célula sentinela.

- Para empilhar um novo item, basta fazer a operação contrária, criando uma nova célula para receber o novo item.

![[Pasted image 20230616121507.png]]

- O campo tam evita a contagem do número de itens no método tamanho.

- Cada célula de uma pilha contém um item da pilha e uma referência para outra célula.

- A classe Pilha contém uma referência para o topo da pilha.

```
public class PilhaDin<T> {
	private Celula topo;
	private long size;
	
	private class Celula {
		T item;
		Celula prox;
		
		public Celula(T item) {
			this.item = item;
		}
	}


	public PilhaDin() { // Cria uma Pilha vazia
//		topo = null;
//		size = 0;
	}

	public void push(T item) {
		if (item == null)
			throw new NullPointerException();
		Celula novo = new Celula(item);
		novo.prox = topo;
		topo = novo;
		size++;
	}

	public T pop() {
		if (vazia())
			throw new RuntimeException("Erro: A pilha esta vazia");
		else {
			T aux = topo.item;
			topo = topo.prox;
			size--;
			return aux;
		}
	}

	public boolean vazia() {
		return (topo == null);
	}

	public long tamanho() {
		return size;
	}
	
}
```

