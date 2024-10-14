
É uma restrição entre dois conjuntos de atributos do banco de dados. Suponha que o esquema de uma base de dados R possua n atributos: A1, A2, ..., An; pense em R = { A1, A2, ... , An } como a representação universal da base de dados.

Uma dependência funcional, representada por X → Y entre dois conjuntos de atributos X e Y que são subconjuntos de R especificam uma restrição nas tuplas que podem compor uma instância relação r de R. 

A restrição estabelece que para qualquer par de tuplas t1 e t2 em r de forma que t1 .[X] = t2 .[X], é obrigado a existir t1 .[Y] = t2 .[Y]. Isto significa que os valores do componente Y em uma tupla em r depende de, ou é determinada pelos valores do componente X. 

Para X → Y lê-se: "Y é funcionalmente dependente de X, ou X infere sobre Y".

## Explicando através da teoria de funções matemáticas

A teoria de funções da matemática pode ser utilizada para explicar a dependência funcional do Modelo Relacional.  Considerando os seguintes conjuntos:

	![[Pasted image 20240812170500.png]]

Observe que existe uma dependência entre os valores dos conjuntos na figura. Essa dependência pode ser expressa pela função f(x) = x + 10, ou seja, y é função de x, ou seja, y = f(x) = x + 10.

Agora, observe os seguintes conjuntos:

	![[Pasted image 20240812170618.png]]

Observe que existe uma dependência entre os valores dos conjuntos, que pode ser expressa pela função f(CPF)=nome. Portanto, nome é função do CPF, ou seja, através de um CPF é possível encontrar o nome da pessoa. Esta dependência é expressa no Modelo Relacional da seguinte maneira: CPF -> NOME.

Seja E uma entidade, e X e Y dois atributos quaisquer de E. Temos que Y é funcionalmente dependente de X se e somente se cada valor de X tiver associado a exatamente um valor de Y.

X -> Y. Leia-se "X determina funcionalmente Y". Exemplo:

	![[Pasted image 20240812171355.png]]


Nesse mesmo contexto (uma empresa de delivery).  O prazo de entrega de um pedido depende do número do pedido: 
	numero→ nome 

- O atributo (numero) que determina o valor é chamado de determinante. O outro atributo (nome) é chamado de dependente. 

- Uma chave primária em uma relação determina funcionalmente todos os outros atributos não-chave na tupla (linha da relação ou tabela).


### Dependência funcional total

- Normalmente uma chave primária (PK) determina funcionalmente todos os atributos não-chaves de uma tupla. 

-  Em uma relação com uma chave primária (PK) composta, um atributo não-chave que dependa dessa PK como um todo, e não somente de parte dela, possui uma Dependência Funcional Total. Exemplo:

	Pedido = (número, data)
		número → data 
	
	Produto = (código, descrição, valorCusto)
		código → {descrição, valorCusto} 
	
	PedidoProduto = (número, código, valorUnitario, quantidade) 
		{número, código} → {valorUnitario, quantidade}



	![[Pasted image 20240813130907.png]]



### Dependência funcional parcial

- Uma Dependência Funcional Parcial ocorre quando os atributos não-chave não dependem funcionalmente de toda chave primária (PK) composta. Sendo assim, existe uma dependência funcional, mas somente de uma parte de PK.  Normalmente isso ocorre quando existe redundância de dados ou algum erro na modelagem. Exemplo:

	![[Pasted image 20240813131727.png]]


![[Pasted image 20240813131912.png]]


Compra = (número, data, situação) 
	número → {data, situação}

Produto = (código, descrição, valorCusto) 
	código → {descrição, valorCusto}

CompraProduto = (número, código, valorUnitario, quantidade, nomeProduto) 
	{número, código} → {valorUnitario, quantidade, nomeProduto}


### Dependência funcional transitiva

Uma Dependência Funcional Transitiva ocorre quando um atributo não depende diretamente da chave primária (PK) composta ou simples, mas depende de um outro atributo não chave. Normalmente isso ocorre quando existe algum erro na modelagem:

	![[Pasted image 20240813133008.png]]