### Quando ocorre?

Essa unchecked exception pode ocorrer ao:
- Chamar um método de uma referência de objeto que esteja com valor nulo
- Acessar ou modificar um atributo de uma referência de objeto nula
- Em caso de array ou coleções, usar métodos de elementos nulos
- Lançar um `NullPointerException`
- Fazer uso de unboxing em um objeto de valor nulo
- Tentar pegar o tamanho de uma array nula

Um exemplo é

```java
public static boolean cartaoExistente(CartaoDeCredito cartaoDeCredito, Usuario usuario) { 
    for (CartaoDeCredito cartao : usuario.getCartoes()) {
        if (cartaoDeCredito.getNumero().equals(cartao.getNumero())) {
            return false;
        }
    }
    return true;
}

public static void main(String[] args) {
    CartaoDeCredito cartaoDeCredito = new CartaoDeCredito("Mário E Alvial", "5152877727714129", "317", LocalDate.of(2019, 6, 9));
    Usuario usuario = new Usuario("Mário Sérgio Esteves Alvial", "75475962820");
    System.out.println(cartaoExistente(cartaoDeCredito, usuario));
}

```

esse código causa um NPE
### Como evitar?

Uma forma deselegante é utilizando `if(x != null)`:

```java
public static boolean cartaoExistente(CartaoDeCredito cartaoDeCredito, Usuario usuario) {
   if (usuario.getCartoes() != null) {
      for (CartaoDeCredito cartao : usuario.getCartoes()) {
         if (cartaoDeCredito.getNumero().equals(cartao.getNumero())) {
            return false;
         }
      }
   }
   return true;
}

```

Se a cada possibilidade de null tivermos de fazer essa verificação, o código fica muito ruim. Porém há outra forma de lidar com isso, chama-se  *programação defensiva*
### Programação Defensiva

Primeiramente, NUNCA atribuir valor de nulo para NADA:

```java
public static Usuario criaUsuario(boolean isMulher) {
	Usuario usuario = null;
	if (isMulher) {
		usuario = criaUsuarioMulher();
	} else {
		usuario = criaUsuarioHomem();
	} return usuario;
  }
```

Dar preferência ao early return

```java
public static Usuario criaUsuario(boolean isMulher){
	if(isMulher) {
		 return criaUsuarioMulher();
	 }
	 return criaUsuarioHomem() 
}
```


Sempre valide dados "não confiáveis". Podemos atribuir esse nome a dados vindos de fontes externas da sua aplicação, seja vindo do usuário ou de uma aplicação externa

Por ultimo e mais importante -> [[Classe Optional]]

