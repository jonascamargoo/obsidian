

Tanto os erros quanto as exceções estendem a classe Throwble, entretanto os erros são lançados pela JVM, fora do controle do programador. É imperioso salientar que os erros são irrecuperáveis, e o compilador sequer nos prepara ou avisa quando emergirão.


![[Pasted image 20240105193629.png]]


##  Checked vs Unchecked

Checked o compilador informa quando uma linha é propensa a interrupção do funcionamento, na unchecked não

![[Pasted image 20240106111915.png]]


##### Checked Exceptions

- Esperadas pelo sistema;
- Verificadas pelo compilador, que obriga a tomar uma atitude: tratar ou declarar(desviar alegando tratamento);
- Estendem Exception diretamente;
- Exemplos: FileNotFoundException.

##### Unchecked Exceptions

- Não esperadas pelo sistema - erro de lógica;
- Não verificada pelo compilador, portanto, não obriga a tomar atitude;
- Estendem a classe RuntimeException, que por sua vez estende Exception;
- Geralmente é impossível a recuperação (erro de lógica evitáveis);
- Exemplos: ArithmeticException, indexOutOfBoundsException, [[NullPointerException (NPE)]]

## Tratando de Exceções (Checked)

Utilizando o Try/Catch. Caso exista o risco de mais de uma exception ser lançada com o nosso código, **podemos fazer mais de um catch**, nomeando cada uma das exceptions separadamente, **dando tratamento específico** (exibindo mensagens ou causas, por exemplo) a cada uma delas:

```java
try {
	//coigo perigoso
} catch (NomeDaException ex) {
	// codigo que trata NomeDaException aqui
} catch (OutraException ex) {
	// codigo que trata OutraException
}
```

 podemos colocar as possíveis exceções no mesmo bloco, separando-as por pipes “|”:

```java
try {
	//coigo perigoso
} catch (NomeDaException | OutraException ex) {
	// codigo ambas as exceções aqui
}
```
 
 Podemos ainda realizar um **catch polimórfico**, pedindo para que seja capturada qualquer exceção que estenda RuntimeException ou até mesmo Exception

```java
try {
	//codigo perigoso aqui
} catch (Exception ex) {
	// codigo que trata exception aqui
}
```
 
 OBS: qualquer caso onde vamos utilizar o multicatch, sempre listamos da mais específica para a mais genérica.

### Bloco finally

Opcional, fica abaixo do catch e tudo que estiver nele será executado, independente da ocorrência - útil para inserir código que necessariamente precisa ser executado.

```java
try {
	//coigo perigoso
} catch (NomeDaException ex) {
	// codigo que trata NomeDaException aqui
} finally {
	// codigo 
}
```


## Delegando para o método acima - Throws

É possível delegar o tratamento ao método que chama aquela exceção utilizando o throw. Nesse caso, ao invés de escrever o bloco try-catch, indicamos na assinatura do método, com a palavra **throws**, a possibilidade do surgimento do evento, nomeando qual ou quais exceptions podem emergir daquele trecho de código - "compilador, estou ciente do risco do surgimento da exceção ‘x’ mas não quero realizar o tratamento. Opto por delegar o tratamento ao chamador do presente método”:

```java
public void metodoArriscado() throws OneExceptionChecked {
	// codigo
}
```

## Lançando Exceções - throw new

O throw new é o **ato de jogar um objeto do tipo exception no topo da pilha de execução**. Apenas com exceções é possível fazer isso. Podemos lançar exceções do tipo checked ou unchecked: as do tipo checked obrigatoriamente virão acompanhadas do bloco try-catch ou da declaração throws na assinatura:

- throw new com unchecked

```java
public void metodoArriscado() {
	throw new OneExceptionUnchecked("deu ruim");
}
```

- throw new com checked (e throws na assinatura)

```java
public void metodoArriscado() throws OneExceptionChecked {
	throw new OneExceptionChecked("deu ruim);
}
```


## Exceções personalizadas

Ao criar a classe da exceção, esta deverá estender de Exception ou RuntimeException, lembrando que, caso estenda Exception será uma exceção personalizada do tipo Checked, e, caso estenda RuntimeException, será uma exceção personalizada do tipo Unchecked

![[Pasted image 20240106121426.png]]


```java
// Definindo uma exceção personalizada
class MinhaExcecaoPersonalizada extends Exception {
    public MinhaExcecaoPersonalizada(String mensagem) {
        super(mensagem);
    }
}

public class ExemploExcecaoPersonalizada {
    // Método que lança a exceção personalizada
    public static void verificarAlgo(int valor) throws MinhaExcecaoPersonalizada {
        if (valor < 0) {
            throw new MinhaExcecaoPersonalizada("O valor não pode ser negativo");
        }
        System.out.println("Valor válido: " + valor);
    }

    public static void main(String[] args) {
        try {
            // Chamando o método que pode lançar a exceção personalizada
            verificarAlgo(-5);
        } catch (MinhaExcecaoPersonalizada e) {
            // Capturando e lidando com a exceção personalizada
            System.out.println("Exceção capturada: " + e.getMessage());
        }
    }
}

```