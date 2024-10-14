Uma Promise podem estar "pendente" (_pending_) ou "resolvida" (_settled_). Os estados possíveis, uma vez que uma Promise está _settled_, são "concluída" (_fulfilled_) ou "rejeitada" (_rejected_). Após passar de _pending_ para _settled_ e se definir como _fulfilled_ ou _rejected_, a Promise não muda mais de estado.

### `Then vs catch`

```js
function getUser(userId) { 
	const userData = fetch(`https://api.com/api/user/${userId}`) 
		.then(response => response.json())
		.then(data => console.log(data.name)) 
}
```


No exemplo acima: ao iniciarmos uma cadeia de promessas - no caso, para fazer uma requisição HTTP - enquanto a resposta está pendente ela retorna um `Promise object`. O objeto, por sua vez, define uma instância do método `.then()`. Ao invés de passar o retorno da função callback diretamente para a função inicial, ela é passada para `.then()`. Quando o resultado da requisição HTTP chega, o corpo da requisição é convertido para JSON e este valor convertido é passado para o próximo método `.then()`.

A cadeia de funções `fetch().then().then()` não significa que há múltiplas funções callbacks sendo usadas com o mesmo objeto de resposta, e sim que cada instância de `.then()` retorna, por sua vez, um `new Promise()`. Toda a cadeia é lida de forma síncrona na primeira execução, e em seguida executada de forma assíncrona.

### `async/await`

Definindo uma função como `async`, podemos utilizar a palavra-chave `await` antes de qualquer expressão que retorne uma promessa. Dessa forma, a execução da função externa (a função `async`) será pausada até que a Promise seja resolvida.

A palavra-chave `await` recebe uma Promise e a transforma em um valor de retorno (ou lança uma exceção em caso de erro). Quando utilizamos `await`, o JavaScript vai aguardar até que a Promise finalize. Se for finalizada com sucesso (o termo utilizado é _fulfilled_), o valor obtido é retornado. Se a Promise for rejeitada (o termo utilizado é _rejected_), é retornado o erro lançado pela exceção.

```js
async function getUser(userId) {
	let response = await fetch(`https://api.com/api/user/${userId}`);
	let userData = await response.json();
	return userData.name;
	 // nas linhas de return não é necessário usar await }
```

Uma função declarada como `async` significa que o valor de retorno da função será, "por baixo dos panos", uma Promise. Se a Promise se resolver normalmente, o objeto-Promise retornará o valor. Caso lance uma exceção, podemos usar o try/catch como estamos acostumados em programas síncronos.

Para executar a função `getUser()`, já que ela retorna uma Promise, pode-se usar `await`

```js
	exibeDadosUser(await getUser(1))
	//ou
	getUser(1).then(exibeDadosUser).catch(reject)
```

### Resolvendo Várias promessas

No caso de várias promessas que devem ser resolvidas para a execução do programa (por exemplo, alguns dados em _endpoints_ REST diferentes), pode-se utilizar `async/await` em conjunto com `Promise.all`:

```js
async function getUser(userId) {
	let response = await fetch(`https://api.com/api/user/${userId}`);
	let userData = await response.json(); return userData;
}

let [user1, user2] = await Promise.all([getUser(1), getUser(2)])

```

###  Há diferenças entre.then() e  async/await?

Em termos de sintaxe, o método `.then()` traz uma sintaxe que faz mais sentido quando utilizamos o JavaScript de forma funcional, enquanto o fluxo das declarações com `async/await` fazem sentido ao serem utilizadas em métodos de classes.

O `async/await` simplifica a escrita e a interpretação do código, mas não é tão flexível e só funciona com uma Promise por vez. Como resolver esse tipo de caso? Exemplo, requisitando uma array de id de pedidos de determinado cliente de um comércio:

```js
async function getCustomerOrders(customerId) {
	const response = await fetch(`https://api.com/api/customer/${customerId}`)
	const customer = await response.json()
	
	return await Promise.all(customer.orders.map(async (orderId) => {
		const response = await fetch(`https://api.com/api/order/${orderId}`)
		const orderData = await response.json()
		
		return orderData.amount
	}))
}
```

No caso acima, usamos `Promise.all` em conjunto com `.map` para fazer todas as requisições, resolver todas as promessas e processar todos os resultados em um único array.

### Iterações com `async/await`

Mas e se precisarmos manejar várias Promises, mas não quisermos fazer isso de uma vez? Um exemplo clássico desta situação é acessar um banco de dados com milhares de registros. Neste caso, não queremos que todas as requisições sejam feitas dessa forma, pois o excesso de requisições simultâneas pode causar problemas de performance e até derrubar o serviço.

Neste caso o `async/await` é mais indicado, pois vai resolver uma Promise por vez.

```js
async function printCustomer(customerId){
	//lógica fictícia da função
}

async function getAndPrintAllCustomers() {
	const sql = 'SELECT id FROM customers'
	const customers = await db.query(sql, [])
	for (const customer of customers) {
		await printCustomer(customer.id)
	}
}


```

No caso acima, não queremos fazer todas as requisições ao banco de uma vez, e sim de forma sequencial - em cada iteração do `for`, o `await` vai resolver uma promessa por vez.