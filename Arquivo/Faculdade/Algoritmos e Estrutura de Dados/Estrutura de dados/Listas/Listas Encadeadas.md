---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

### Lista Encadeada

### Definição

- **Listas Encadeadas**: Em listas encadeadas, a ordem dos elementos na lista não implica necessariamente em que eles sejam armazenados de forma consecutiva na memória. A ordem é lógica e é definida pela forma como os elementos estão interligados.
    
- Cada item da lista contém informações que permitem alcançar o próximo item na sequência. Cada elemento armazena uma referência (ponteiro) para o próximo elemento da lista.
    
- Na implementação de listas encadeadas, é necessário armazenar separadamente a informação do primeiro elemento da lista, chamado de nó cabeça (head node), pois ele serve como ponto de partida para percorrer a lista.
    
- Uma das vantagens das listas encadeadas é que é possível inserir e retirar elementos sem a necessidade de deslocar os itens seguintes da lista, o que pode ser uma operação custosa em listas lineares.
    
- Existem duas formas de representar listas encadeadas: através de arrays (denominada lista encadeada estática) ou por referências (ponteiros, denominada lista encadeada dinâmica). A escolha entre essas representações depende das necessidades específicas do problema e dos recursos disponíveis.
    

As listas encadeadas são particularmente úteis em situações em que a alocação dinâmica de memória é necessária e quando a ordem lógica dos elementos é mais importante do que a sua disposição física na memória. Elas são amplamente usadas em estruturas de dados e algoritmos, como pilhas, filas e representações de grafos, onde a flexibilidade na alocação e liberação de memória é crucial.

#### Vantagens vs desvantagens

- Vantagens
	-  Elimina o problema dos deslocamentos de células
	- Não é necessário saber previamente o número de elementos a serem armazenados (lista dinâmica)
- Desvantagens
	-  Não se consegue acessar os elementos da lista em tempo constante
	-  Mais operações para manter integridade dos dados

>>> Lista encadeada estática

![[Pasted image 20230607105205.png]]


###  ---------- Listas Encadeadas Dinâmicas (LED) ----------------

- Cada item da lista é encadeado com o seguinte através de uma variável de referência (ponteiro);

- Esta implementação permite utilizar posições não contíguas de memória, sendo possível inserir e retirar elementos sem deslocar os itens da lista;

- A lista é constituída de células, onde cada célula contém um item da lista e um apontador para a célula seguinte;

- É conveniente utilizar listas encadeadas dinâmicas em aplicações em que não existe previsão sobre o crescimento da lista, por não ser necessário definir o tamanho da lista a priori;

#### Características

##### Sobre as células da lista
- Células não estão contíguas na memória

![[Pasted image 20230607105651.png]]


- Célula: guarda as informações sobre cada elemento;
- Para isso define-se cada célula como uma estrutura que possui:
	-  Campos de informações
	-  Ponteiro (referência) para a próxima célula


				![[Pasted image 20230607105754.png]]


- Uma lista pode ter uma célula cabeça (head)

![[Pasted image 20230607110339.png]]

- Uma lista pode ter um apontador para o último elemento (tail)

- Criando lista vazia

					![[Pasted image 20230607110447.png]]


#### Inserção de Elementos na Lista
 - Podem ser feitas no início, meio e fim
 - No início:  ![[Pasted image 20230607110642.png]]

- Na ultima: ![[Pasted image 20230607110900.png]]

- Após elemento E: ![[Pasted image 20230607110928.png]]

	Aqui vemos que após encontrar a posição (temporariamente chamada de aux) o newCell.next (parte superior do triangulo) recebe a ref do aux.prox. Por fim, o newCell desce e entra na lista, sendo encadeado à traseira de aux.

#### Retirada de Elementos na Lista

- Na primeira posição: ![[Pasted image 20230607111054.png]]

- Retirada do elemento E: ![[Pasted image 20230607111124.png]]

- Retirada do último elemento da lista: 
![[Pasted image 20230607111155.png]]


#### Operações

Poderia utilizar o get para as checagem, mas não o fim (já tinha feito e nem sei se é melhor)

```

public class LED {

    class Cell {
        Object item;
        Cell next;
    }

    private Cell head;

    public LED() {}

    // Adiciona um item no final da lista
    void add(Object item) {
        if (head == null) {
            head = new Cell();
            head.item = item;
        } else {
            Cell aux = head;
            while (aux.next != null) {
                aux = aux.next;
            }
            Cell newCell = new Cell();
            newCell.item = item;
            aux.next = newCell;
        }
    }

    // Insere um item no início da lista
    void insert(Object item) {
        Cell newCell = new Cell();
        newCell.item = item;

        if (head == null) {
            head = newCell;
        } else {
            newCell.next = head;
            head = newCell;
        }
    }

    // Insere um item na i-ésima posição da lista
    void insert(Object item, int i) {
        if (i < 0) {
            throw new ArrayIndexOutOfBoundsException("Índice inválido: " + i);
        }

        Cell newCell = new Cell();
        newCell.item = item;

        if (i == 0) {
            newCell.next = head;
            head = newCell;
        } else {
            Cell aux = head;
            int count = 0;

            while (count < i - 1 && aux != null) {
                aux = aux.next;
                count++;
            }

            if (aux == null) {
                throw new ArrayIndexOutOfBoundsException("Índice inválido: " + i);
            }

            newCell.next = aux.next;
            aux.next = newCell;
        }
    }

    // Exclui o nó na i-ésima posição da lista
    void delete(int i) {
        if (i < 0 || head == null) {
            throw new ArrayIndexOutOfBoundsException("Índice inválido: " + i);
        }

        if (i == 0) {
            head = head.next;
            return;
        }

        Cell previous = null;
        Cell current = head;
        int currenti = 0;

        while (current != null && currenti < i) {
            previous = current;
            current = current.next;
            currenti++;
        }

        if (current != null) {
            // Excluir o nó na posição especificada
            previous.next = current.next;
        }
    }

    // Exclui o nó que contém o item especificado
    void deleteByItem(Object item) {
        if (head == null) {
            throw new ArrayIndexOutOfBoundsException("Item inválido: " + item);
        }

        if (head.item == item) {
            // O item a ser removido está no primeiro nó
            head = head.next;
            return;
        }

        Cell previous = null;
        Cell current = head;

        while (current != null && !current.item.equals(item)) {
            previous = current;
            current = current.next;
        }

        if (current != null) {
            // O item foi encontrado, removemos o nó
            previous.next = current.next;
        }
    }

	@Override
	public String toString() {
	    StringBuilder sb = new StringBuilder("[ ");
	    Cell aux = head;
	
	    while (aux != null) {
	        sb.append(aux.item);
	        sb.append(" ");
	        aux = aux.next;
	    }
	
	    sb.append("]");
	    return sb.toString();
	}

}

```


#### Vantagens vs desvantagens

- Vantagens:
	-  Permite inserir ou retirar itens do meio da lista a um custo constante (importante quando a lista tem de ser mantida em ordem).
	- Bom para aplicações em que não existe previsão sobre o crescimento da lista (o tamanho máximo da lista não precisa ser definido a priori).

- Desvantagem:
	- Utilização de memória extra para armazenar os apontadores.
	


### Lista simplesmente encadeada com sentinela
- Sentinel é um nó especial adicionado no início ou no final da lista para simplificar a implementação e melhorar a eficiência de certas operações.

- O nó sentinela não contém nenhum dado relevante para a aplicação em si, mas é usado como uma marcação ou referência;

- Com um sentinel, você não precisa verificar explicitamente se a lista está vazia ou se está lidando com o primeiro ou último elemento da lista

- Nodos especiais header e tail
	- Não armazenam elementos
	- header possui campo lig_prev nulo (NULL)
	- tail possui campo lig_next nulo (NULL)

![[Pasted image 20230608113914.png]]

#### Operações

```
public class LEDS<T> {
	private Celula head;
	private Celula tail;
	private long size;

	// classe interna
	private class Celula {
		T item;
		Celula prox;

		public Celula() {
		}

		public Celula(T item) {
			this.item = item;
		}
	}

	public LEDS() {
		head = new Celula(); // sentinela
		tail = head;
	}

	// adiciona
	public void add(T item) {
		if (item != null) {
			tail.prox = new Celula(item);
			tail = tail.prox;
			size++;
		}
	}


	public T get(long indice) {
		if (indice >= 0 && indice < size) {
			long cont = 0;
			Celula aux = head.prox;
			while (cont < indice) {
				cont++;
				aux = aux.prox;
			}
			return aux.item;
		} else
			throw new ArrayIndexOutOfBoundsException("Índice invál: " + indice);
	}

	public String toString() {
		StringBuilder sb = new StringBuilder("[ ");
		Celula aux = head.prox;

		while (aux != null) {
			sb.append(aux.item);
			sb.append(" ");
			aux = aux.prox;
		}
		sb.append("]");
		return sb.toString();
	}
}

```

### Lista simplesmente encadeada com tail

```

public class LEDTail {

    // Classe interna
    private class Cell {
        String item;
        Cell next;

        public Cell(String item) {
            this.item = item;
        }
    }

    private Cell head;
    private Cell tail;
    private long size;

    // Criando lista vazia
    public LEDTail() {
        head = null;
        tail = null;
        size = 0;
    }

    public long getSize() {
        return size;
    }

    // Adicionar no final da lista - complexidade O(1)
    public void add(String item) {
        if (item == null) {
            throw new NullPointerException("Objeto a ser adicionado é nulo");
        }

        Cell newCell = new Cell(item);
        if (head == null) {
            head = newCell;
        } else {
            tail.next = newCell;
        }
        tail = newCell;
        size++;
    }

    // Inserir no início da lista - complexidade O(1)
    public void insert(String item) {
        if (item == null) {
            throw new NullPointerException("Objeto a ser adicionado é nulo");
        }

        Cell newCell = new Cell(item);
        newCell.next = head;
        head = newCell;
        if (tail == null) {
            tail = newCell;
        }
        size++;
    }

    // Inserir na posição específica - complexidade O(n)
    public void insert(String item, int position) {
        if (item == null) {
            throw new NullPointerException("Objeto a ser adicionado é nulo");
        }

        if (position < 0 || position > size) {
            throw new IndexOutOfBoundsException("Posição inválida: " + position);
        }

        if (position == 0) {
            insert(item);
            return;
        }

        Cell newCell = new Cell(item);
        Cell current = head;
        for (int i = 0; i < position - 1; i++) {
            current = current.next;
        }
        newCell.next = current.next;
        current.next = newCell;
        if (current == tail) {
            tail = newCell;
        }
        size++;
    }

    // Excluir pela posição - complexidade O(n)
    public String excluir(int position) {
        if (head == null) {
            throw new IllegalArgumentException("Lista vazia");
        }

        if (position < 0 || position >= size) {
            throw new IndexOutOfBoundsException("Posição inválida: " + position);
        }

        Cell excluido;
        if (position == 0) {
            excluido = head;
            head = head.next;
            if (head == null) {
                tail = null;
            }
        } else {
            Cell aux = head;
            for (int i = 0; i < position - 1; i++) {
                aux = aux.next;
            }
            excluido = aux.next;
            aux.next = excluido.next;
            if (aux.next == null) {
                tail = aux;
            }
        }
        size--;
        return excluido.item;
    }

    // Excluir pelo valor - complexidade O(n)
    public String excluir(String item) {
        if (head == null) {
            throw new IllegalArgumentException("Lista vazia");
        }

        if (head.item.equals(item)) {
            return excluir(0);
        }

        Cell aux = head;
        while (aux.next != null && !aux.next.item.equals(item)) {
            aux = aux.next;
        }

        if (aux.next == null) {
            throw new IllegalArgumentException("Item não encontrado");
        }

        Cell excluido = aux.next;
        aux.next = excluido.next;
        if (aux.next == null) {
            tail = aux;
        }
        size--;
        return excluido.item;
    }

    // Copiar a lista - complexidade O(n)
    public LEDTail copiar() {
        LEDTail newList = new LEDTail();

        Cell aux = head;
        while (aux != null) {
            newList.add(aux.item);
            aux = aux.next;
        }

        return newList;
    }

    // Obter item pela posição - complexidade O(n)
    public String get(int position) {
        if (position < 0 || position >= size) {
            throw new IndexOutOfBoundsException("Posição inválida: " + position);
        }

        Cell aux = head;
        for (int i = 0; i < position; i++) {
            aux = aux.next;
        }

        return aux.item;
    }

	@Override
	public String toString() {
	    StringBuilder sb = new StringBuilder();
	    sb.append('[');
	
	    if (head != null) {
	        Cell aux = head;
	        while (aux != null) {
	            sb.append(aux.item);
	            sb.append(' ');
	            aux = aux.next;
	        }
	        sb.deleteCharAt(sb.length() - 1); // apagando o último espaço
	    }
	
	    sb.append(']');
	
	    return sb.toString();
	}


}



```



### Lista Duplamente Encadeadas Dinâmica (LDED)

- Listas simplesmente encadeadas são ineficientes para realizar certas operações. Por exemplo:
	- Remover o último elemento ou um elemento intermediário: 
		- É preciso percorrer toda lista para encontrar o elemento anterior

- Muitas aplicações não demandam tais operações. P.ex:
	- Pilhas e filas podem ser implementadas eficientemente apenas removendo elementos do início de uma lista

- E quando tais operações são necessárias?
	- Podemos utilizar uma lista duplamente encadeada

- Cada elemento da lista possui informações de quem é seu sucessor e antecessor
- Cada célula armazena:
	- elemento (registro, objeto, ...);
	- ponteiro para a próxima célula;
	- ponteiro para a célula anterior;

	![[Pasted image 20230608113211.png]]

 ![[Pasted image 20230608113236.png]]

```
public class LDEDS<T> {
    class Celula {
        T item; // qualquer tipo
        Celula prox;
        Celula ant;

        public Celula(T item) {
            this.item = item;
        }
    }

    private Celula head;
    private Celula tail;
    private long size;

    // construtor
    public LDEDS() {
        head = new Celula(null); // sentinela
        tail = new Celula(null); // sentinela
        head.prox = tail;
        tail.ant = head;
    }

    // insere item no final O(1)
    public void add(T item) {
        Celula novo = new Celula(item);
        novo.ant = tail.ant;
        novo.prox = tail;
        tail.ant = novo;
        novo.ant.prox = novo;
        size++;
    }

    public void add(int indice, T item) {
        if (indice < 0 || indice > size) {
            throw new ArrayIndexOutOfBoundsException("Índice invál: " + indice);
        }

        if (indice == size) {
            add(item); // Adiciona no final
        } else {
            Celula aux = getCell(indice);
            Celula novo = new Celula(item);
            novo.ant = aux.ant;
            novo.prox = aux;
            aux.ant.prox = novo;
            aux.ant = novo;
            size++;
        }
    }

    public T excluir(T item) {
        if (head.prox == tail) {
            throw new IllegalArgumentException("Lista vazia");
        } else {
            Celula aux = head.prox;
            while (aux != tail && !aux.item.equals(item)) {
                aux = aux.prox;
            }
            if (aux == tail) {
                throw new IllegalArgumentException("Item não encontrado");
            } else {
                aux.ant.prox = aux.prox;
                aux.prox.ant = aux.ant;
                size--;
                return aux.item;
            }
        }
    }

    public T excluir(int indice) {
        if (indice < 0 || indice >= size) {
            throw new ArrayIndexOutOfBoundsException("Índice invál: " + indice);
        }

        Celula aux = getCell(indice);
        aux.ant.prox = aux.prox;
        aux.prox.ant = aux.ant;
        size--;
        return aux.item;
    }

    private Celula getCell(int indice) {
        Celula aux;
        if (indice < size / 2) {
            aux = head.prox;
            for (int i = 0; i < indice; i++) {
                aux = aux.prox;
            }
        } else {
            aux = tail.ant;
            for (int i = size - 1; i > indice; i--) {
                aux = aux.ant;
            }
        }
        return aux;
    }

    public String toString() {
        StringBuilder sb = new StringBuilder("[ ");
        Celula aux = head.prox;

        while (aux != tail) {
            sb.append(aux.item);
            sb.append(" ");
            aux = aux.prox;
        }
        sb.append("]");
        return sb.toString();
    }
}

```


### Lista circular

- Na lista circular, o último nó aponta para o primeiro nó.
	- A lista pode ou não ter um nó cabeça.
- As listas circulares são usadas em escalonamento de processos
- Geralmente é usada em situações onde é necessário caminhar continuamente pela lista.

- Uma lista circular não tem um primeiro nó nem último nó “naturais”
	- Uma convenção útil é apontar o ponteiro externo (“tail” para a lista circular) para o último nó, sendo o conceito de último vindo de tempo de inclusão
- O ponteiro head torna-se permanentemente aterrado e o ponteiro tail aponta o último elemento da lista

- Outra alternativa consiste em usar apenas um ponteiro externo head

![[Pasted image 20230608124835.png]]

- Listas circulares podem ser simples ou duplamente encadeadas

![[Pasted image 20230608124906.png]]

#### Operações

```
public class LCDE<T> {
    class Celula {
        T item; // qualquer tipo
        Celula prox;
        Celula ant;

        public Celula(T item) {
            this.item = item;
        }
    }

    private Celula head;
    private long size;

    public void add(T item) {
        if (head == null) {
            head = new Celula(item);
            head.prox = head;
            head.ant = head;
        } else {
            Celula novo = new Celula(item);
            novo.prox = head;
            novo.ant = head.ant;
            head.ant.prox = novo;
            head.ant = novo;
        }
        size++;
    }

    public T get(int posicao) {
        if (posicao < 0 || posicao >= size) {
            throw new IndexOutOfBoundsException("Posição inválida: " + posicao);
        }
        Celula aux = head;
        for (int i = 0; i < posicao; i++) {
            aux = aux.prox;
        }
        return aux.item;
    }

    public T remove() {
        if (head == null) {
            throw new IllegalStateException("Lista vazia");
        }
        T item = head.item;
        if (head.prox == head) {
            head = null;
        } else {
            head.ant.prox = head.prox;
            head.prox.ant = head.ant;
            head = head.prox;
        }
        size--;
        return item;
    }

    public long size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public String toString() {
        StringBuilder sb = new StringBuilder("[ ");
        if (head != null) {
            Celula aux = head;
            do {
                sb.append(aux.item);
                sb.append(" ");
                aux = aux.prox;
            } while (aux != head);
        }
        sb.append("]");
        return sb.toString();
    }
}

```