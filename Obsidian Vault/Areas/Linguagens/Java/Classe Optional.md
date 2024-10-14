
## O que é?

O propósito do `Optional` é fornecer uma abordagem mais explícita e segura para representar valores que podem ou não estar presentes, em vez de permitir nulos diretamente. Ele força o programador a considerar o caso de ausência de um valor e, assim, reduzir erros relacionados a nulos.
## Por que usar?


1. **Evita NullPointerExceptions:** O `Optional` fornece métodos que ajudam a evitar NullPointerExceptions, obrigando o programador a verificar se um valor está presente antes de tentar acessá-lo.
    
2. **Fluente e Encadeável:** As operações com `Optional` são encadeáveis e fluídas. Você pode encadear operações de forma mais legível e concisa.
    
3. **Tratamento de Valores Nulos:** O `Optional` pode ser utilizado para encapsular valores que podem ser nulos, permitindo uma manipulação mais segura desses valores.
    
4. **Expressividade no Código:** O uso de `Optional` torna o código mais expressivo, indicando claramente que um valor pode estar ausente e forçando a consideração explícita desse cenário.


## Como usar?

### Criando objetos Optional

Para criar um objeto Optional empty

`Optional<String> empty = Optional.empty();`


Para criar um objeto Optional de name

```java
String name = "baeldung";
Optional<String> opt = Optional.of(name);
assertTrue(opt.isPresent());
```


Agora, verifica se um `Optional` criado a partir de uma variável que pode ser nula (`name`) está presente, ou seja, se contém um valor não nulo. Se `name` não for nulo, o `Optional` estará presente, e o teste passará.

```java
@Test
public void givenNonNull_whenCreatesNullable_thenCorrect() {
    String name = "baeldung";
    Optional<String> opt = Optional.ofNullable(name);
    assertTrue(opt.isPresent());
}
```


### Verificando se o valor em questão está presente ou não

```java
@Test
public void givenOptional_whenIsPresentWorks_thenCorrect() {
    Optional<String> opt = Optional.of("Baeldung");
    assertTrue(opt.isPresent());

    opt = Optional.ofNullable(null);
    assertFalse(opt.isPresent());
}


// tb tem o isEmpty() a partir do java 11
@Test
public void givenAnEmptyOptional_thenIsEmptyBehavesAsExpected() {
    Optional<String> opt = Optional.of("Baeldung");
    assertFalse(opt.isEmpty());

    opt = Optional.ofNullable(null);
    assertTrue(opt.isEmpty());
}
```


### Conditional Action With _ifPresent()_


Em vez de checar se algo é nulo, podemos usar o ifPresent():

```java
// em vez disso
if(name != null) {
    System.out.println(name.length());
}

// podemos fazer isso


Optional<String> opt = Optional.of("baeldung");
opt.ifPresent(name -> System.out.println(name.length()));

```


### Métodos orElse() e orElseGet()
#### Valor padrão com orElse()

O método `orElse()` é utilizado para recuperar o valor encapsulado dentro de uma instância de Optional. Ele recebe um parâmetro que atua como um valor padrão. O método `orElse()` retorna o valor encapsulado se estiver presente e, caso contrário, retorna o valor do argumento fornecido:

```java
@Test
public void whenOrElseWorks_thenCorrect() {
    String nullName = null;
    String name = Optional.ofNullable(nullName).orElse("john");
    assertEquals("john", name);
}
```

Cria um `Optional` a partir de `nullName` usando `ofNullable` e, em seguida, utiliza `orElse("john")`. Se o `Optional` estiver vazio (no caso de `nullName` ser nulo), ele retorna "john"

#### Valor padrão com  orElseGet()

O método `orElseGet()` é semelhante ao `orElse()`. No entanto, em vez de receber um valor para retornar se o valor do Optional não estiver presente, ele recebe um fornecedor (supplier) de uma interface funcional. Esse fornecedor é invocado e retorna o valor da invocação:

```java
@Test
public void whenOrElseGetWorks_thenCorrect() {
    String nullName = null;
    String name = Optional.ofNullable(nullName).orElseGet(() -> "john");
    assertEquals("john", name);
}
```


Cria um `Optional` a partir de `nullName` usando `ofNullable` e, em seguida, utiliza `orElseGet(() -> "john")`. Se o `Optional` estiver vazio (no caso de `nullName` ser nulo), ele invoca o fornecedor (lambda `() -> "john"`) para obter o valor "john".

#### Diferença entre orElse() e orElseGet()

Apesar de similar, há uma importante diferença de performance, analisemos:

```java
public String getMyDefault() {
    System.out.println("Getting Default Value");
    return "Default Value";
}

@Test
public void whenOrElseGetAndOrElseOverlap_thenCorrect() {
    String text = null;

    String defaultText = Optional.ofNullable(text).orElseGet(this::getMyDefault);
    assertEquals("Default Value", defaultText);

    defaultText = Optional.ofNullable(text).orElse(getMyDefault());
    assertEquals("Default Value", defaultText);
}
```

No exemplo acima, encapsulamos um texto nulo dentro de um objeto Optional e tentamos obter o valor encapsulado usando cada uma das duas abordagens. O método `getMyDefault()` é chamado em cada caso. Acontece que quando o valor encapsulado não está presente, tanto `orElse()` quanto `orElseGet()` funcionam exatamente da mesma maneira. O output seria:

```bash
Getting default value...
Getting default value...
```

Agora, vamos executar outro teste em que o valor está presente, e idealmente, o valor padrão nem deveria ser criado:

```java
@Test
public void whenOrElseGetAndOrElseDiffer_thenCorrect() {
    String text = "Text present";

    System.out.println("Using orElseGet:");
    String defaultText  = Optional.ofNullable(text).orElseGet(this::getMyDefault);
    assertEquals("Text present", defaultText);

    System.out.println("Using orElse:");
    defaultText = Optional.ofNullable(text).orElse(getMyDefault());
    assertEquals("Text present", defaultText);
}
```

```bash
Using orElseGet:
Using orElse:
Getting default value...
```

No exemplo acima, não estamos mais encapsulando um valor nulo, e o restante do código permanece o mesmo. Observe que ao usar `orElseGet()` para recuperar o valor encapsulado, o método `getMyDefault()` nem mesmo é invocado, uma vez que o valor contido está presente. No entanto, ao usar `orElse()`, quer o valor encapsulado esteja presente ou não, o objeto padrão é criado. Portanto, neste caso, acabamos criando um objeto redundante que nunca é utilizado.

Neste exemplo simples, não há um custo significativo na criação de um objeto padrão, pois a JVM sabe como lidar com isso. No entanto, quando um método como `getMyDefault()` precisa fazer uma chamada a um serviço web ou até mesmo consultar um banco de dados, o custo torna-se muito evidente.

### Exceções com orElseThrow()

Parecido com o orElse() e orElseGet(), em vez de retornar um valor padrão, lança uma exceção

```java
// java < 10
@Test(expected = IllegalArgumentException.class)
public void whenOrElseThrowWorks_thenCorrect() {
    String nullName = null;
    String name = Optional.ofNullable(nullName).orElseThrow(IllegalArgumentException::new);
}

// java >= 10
@Test(expected = NoSuchElementException.class)
public void whenNoArgOrElseThrowWorks_thenCorrect() {
    String nullName = null;
    String name = Optional.ofNullable(nullName).orElseThrow();
}
```


Para saber mais https://www.baeldung.com/java-optional