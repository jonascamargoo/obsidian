---
tipo: conceito
area: Algoritmos e Estrutura de Dados
tags:
- algoritmos
criada: '2024-10-14'
---

### Definição

Listas lineares são uma das formas mais simples de organizar elementos em um conjunto. Elas são estruturas de dados que oferecem operações para inserir, retirar e localizar elementos. O tamanho dessas listas pode crescer ou diminuir durante a execução de um programa, conforme necessário. Elas permitem que os itens sejam acessados, inseridos ou retirados de forma flexível. Além disso, é possível concatenar duas listas para criar uma única lista ou dividir uma lista em duas ou mais partes. As listas lineares são especialmente úteis quando não é possível prever a demanda de memória, permitindo a manipulação de quantidades variáveis de dados com formatos imprevisíveis. São aplicadas em diversas áreas, como manipulação simbólica, gerenciamento de memória, simulações e desenvolvimento de compiladores.

- Sequência de zero ou mais itens
	x1 , x2 ,···, x n , na qual x i é de um determinado tipo e n
	representa o tamanho da lista linear.
	
- Sua principal propriedade estrutural envolve as posições relativas dos itens em uma dimensão.
	- Assumindo n ≥ 1, x 1 é o primeiro item da lista e x n é o último item da lista.
	
		– xi precede xi+1 para i = 1, 2, ···, n–1
		– xi sucede xi-1 para i = 2, 3,···,n
		– o elemento xi é dito estar na i-ésima posição da lista
#### Tad de listas lineares

- O que deveria conter?
	 Representação do tipo da lista
	 Conjunto de operações que atuam sobre a lista
	 
- Algumas operações que deveriam fazer parte deste conjunto?
	- Um conjunto de operações necessário a uma maioria de aplicações é:
		- Criar uma lista linear vazia;
		-  Inserir um novo item imediatamente após o i-ésimo item;
		-  Retirar o i-ésimo item;
		-  Localizar o i-ésimo item para examinar e/ou alterar o conteúdo de seus
		componentes;
		-  Combinar duas ou mais listas lineares em uma lista única;
		-  Dividir uma lista linear em duas ou mais listas;
		-  Fazer uma cópia da lista linear;
		-  Ordenar os itens da lista em ordem ascendente ou descendente, de acordo
		com alguns de seus componentes;
		-  Pesquisar a ocorrência de um item com um valor particular em algum
		componente.

- Exemplo de protótipo para operações:
	- FLVazia(Lista). Faz a lista ficar vazia;
	- LInsere(x, Lista). Insere x após o último item da lista;
	- LRetira(p, Lista, x). Retorna o item x que está na posição p da lista, retirando-o da lista e deslocando os itens a partir da posição p+1 para as posições anteriores;
	- LEhVazia(Lista). Esta função retorna true se lista vazia, senão retorna false;
	- LImprime(Lista). Imprime os itens da lista na ordem de ocorrência.

#### Implementação de listas lineares

- Várias estruturas de dados podem ser usadas para representar listas lineares, cada uma com vantagens e desvantagens particulares.
- As duas representações mais utilizadas são as implementações por meio de arranjos e de apontadores

##### Implementação de listas lineares com arranjos

- Os itens da lista são armazenados em posições contíguas de memória.
- A lista pode ser percorrida em qualquer direção.
- A inserção de um novo item pode ser realizada após o último item com custo constante.
- A inserção de um novo item no meio da lista requer um deslocamento de todos os itens localizados após o ponto de inserção.
- Retirar um item do início da lista requer um deslocamento de itens para preencher o espaço deixado vazio.
- 
![[Pasted image 20230606105657.png]]

##### Estrutura da lista usando arranjo

- Os itens são armazenados em um array de tamanho suficiente para armazenar a lista.
- O campo Último aponta para a posição seguinte a do último elemento da lista.
- O i-ésimo item da lista está armazenado na (i - 1)-ésima posição do array, 0 ≤ i < Último.
- A constante MaxTam define o tamanho máximo permitido para a lista.

##### Operações sobre Lista Usando Arranjo

```
public class ListaEstatic {
	private Object[] item;
	private int ultimo, pos;
		
	//fazer lista vazia
	public ListaEstatica(int tamMax) {
		ultimo = 0;
		pos = 0;
		item = new Object[tamMax];
	}
	
	public void insere(Objetc item) {
		if(ultimo < this.item.lenght) {
			this.item[ultimo] = item;
			ultimo++;
		} else {
			throw new IllegalArgumentException("Lista cheia");
		}
	}
	
	public void insere(int posicao, Object item) {
	    if (posicao > ultimo) {
	        insere(item);
	        return;
	    }
	    
	    if (ultimo >= this.item.length) {
	        throw new IllegalArgumentException("Lista cheia");
	    }
	    
	    for (int i = ultimo; i > posicao; i--) {
	        this.item[i] = this.item[i - 1];
	    }
	    
	    this.item[posicao] = item;
	    ultimo++;
	}
	
	public Object retira(Object chave) {
	    if (vazia() || chave == null) {
	        throw new IllegalArgumentException("Erro: A lista está vazia");
	    }
	    
	    int p = 0;
	    boolean chaveEncontrada = false;
	    
	    for (; p < ultimo; p++) {
	        if (item[p].equals(chave)) {
	            chaveEncontrada = true;
	            break;
	        }
	    }
	    
	    if (!chaveEncontrada) {
	        return null; // chave não encontrada
	    }
	    
	    Object itemEncontrado = item[p];
	    ultimo--;
	    
	    for (int aux = p; aux < ultimo; aux++) {
	        item[aux] = item[aux + 1];
	    }
	    
	    return itemEncontrado;
	}
	
	public boolean vazia() {
		return (ultimo)
	}
	
	public void imprime() {
		System.out.println();
		for(int aux = ; aux < ultimo; aux++) {
			System.out.print(item[aux].toString()+"\t");
		}
	}
}	

```


##### Tamanho dinâmico:

Toda lista linear é inicialmente estática, porém, em sua implementação, cria-se um mecanismo para deixá-la dinâmica.
Exemplo disso é  o ArrayList em Java. A classe possui duas propriedades, o `tamanho` (valor 10) e o elemento `data`, sendo este genérico e esse abstrato. Ao passo que a lista atinge a capacidade máximo de elementos, cria-se um novo objeto com o `tamanho` incrementado (valor 20) e todos os elementos da lista antiga são copiados para essa lista nova. Esse comportamento tomar a operação add() `O(1)` no melhor caso e `O(n)` no pior caso, em que tem-se de criar nova lista.

Além disso, add(meio) é `O(n)` pois consiste em copiar os itens subsequentes (arredar), para remove() também - exceto remoção no fim, pois não precisamos arredar nenhum elemento pois ele já é inserido no fim.

Ou seja, sempre que temos de arredar posições aqui, é `O(n)`

##### Vantagens vs desvantagens

- Vantagem: (Relativa)
	- economia de memória (os apontadores são implícitos nesta estrutura).

- Desvantagens:
	-  custo para inserir ou retirar itens da lista pode causar um deslocamento de todos os itens no pior caso;
	- em aplicações em que não existe previsão sobre o crescimento da lista, a utilização de arranjos em linguagens como o Pascal, C, Java pode ser problemática porque neste caso o tamanho máximo da lista tem de ser definido em tempo de compilação.