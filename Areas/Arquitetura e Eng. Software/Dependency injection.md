## O que é?
	Quando uma classe A usa uma funcionalidade da classe B, temos uma dependência de A por B. Em POO, para utilizar um método de uma classe, precisamos antes instanciar um objeto daquela mesma classe. Assim, transferir a tarefa de criar o objeto para outra pessoa e usar diretamente a dependência é chamado de injeção de dependência.

## Por que utilizar?

```
class car {
	private Wheels wheel = new MRFWheels();
	private Battery battery = new ExcideBattery();
}
```
	
	Aqui a classe car é responsável por criar todos os objetos de dependência. Agora, e se decidirmos abandonar o MRFWheels no futuro e quisermos usar o Yokohama Wheels? Precisamos recriar o objeto car com uma nova dependência de Yokohama. Mas ao usar injeção de dependência (DI), podemos alterar as rodas em tempo de execução (porque as dependências podem ser injetadas em tempo de execução e não em tempo de compilação). Existem basicamente três tipos de injeção de dependência:

Sem injeção:

```
public class Client {
    private Service service;

    Client() {
        // The dependency is hard-coded.
        this.service = new ExampleService();
    }
}
```


## Roles

### Service and client
	Um service é qualquer classe que contém funcionalidade útil. Por sua vez, um client é qualquer classe que usa service. Os service que um cliente requer são as dependências do cliente. Qualquer objeto pode ser um service ou um client; os nomes referem-se apenas ao papel que os objetos desempenham em uma injeção. O mesmo objeto pode até ser tanto um client (ele usa services injetados) quanto um service (ele é injetado em outros objetos). Após a injeção, o service se torna parte do estado do cliente, disponível para uso.

### Interfaces
	Os clients não devem saber como suas dependências são implementadas, apenas seus nomes e API. Um serviço que recupera e-mails, por exemplo, pode usar os protocolos IMAP ou POP3 nos bastidores, mas esse detalhe provavelmente é irrelevante para o código de chamada que apenas deseja que um e-mail seja recuperado. Ao ignorar os detalhes da implementação, os clientes não precisam mudar quando suas dependências o fazem.

### Injectors
	O injetor, às vezes também chamado de montador, conteiner, fornecedor ou fábrica, apresenta serviços ao cliente. O papel dos injetores é construir e conectar grafos de objetos complexos, onde os objetos podem ser clientes e serviços. O próprio injetor pode ser muitos objetos trabalhando juntos, mas não deve ser o cliente, pois isso criaria uma dependência circular. Como a injeção de dependência separa como os objetos são construídos de como eles são usados, geralmente diminui a importância da 'new' palavra-chave encontrada na maioria das linguagens orientadas a objetos. Como a estrutura lida com a criação de serviços, o programador tende a construir diretamente apenas objetos de valor que representam entidades no domínio do programa (como um objeto Employee em um aplicativo de negócios ou um objeto Order em um aplicativo de compras


## Analogia
	Como analogia, os carros podem ser pensados como serviços que executam o trabalho útil de transportar pessoas de um lugar para outro. Os motores dos carros podem exigir gasolina, diesel ou eletricidade, mas esse detalhe não é importante para o cliente - um motorista - que só se importa se pode levá-los ao seu destino. Os carros apresentam uma interface uniforme por meio de seus pedais, volantes e outros controles. Como tal, o motor com o qual eles foram 'injetados' na linha de fábrica deixa de importar e os motoristas podem alternar entre qualquer tipo de carro conforme necessário.

## Tipos de DI

1. injeção de construtor: as dependências são fornecidas por meio de um construtor de classe. A forma mais comum de injeção de dependência é uma classe solicitar suas dependências por meio de seu construtor. Isso garante que o cliente esteja sempre em um estado válido, pois não pode ser instanciado sem suas dependências necessárias:

```
public class Client {
    private Service service;

    // The dependency is injected through a constructor.
    Client(Service service) {
        if (service == null) {
            throw new IllegalArgumentException("service must not be null");
        }
        this.service = service;
    }
}
```

3. injeção de setter: o cliente expõe um método setter que o injetor usa para injetar a dependência. Ao aceitar dependências por meio de um método setter, em vez de um construtor, os clientes podem permitir que os injetores manipulem suas dependências a qualquer momento. Isso oferece flexibilidade, mas torna difícil garantir que todas as dependências sejam injetadas e válidas antes que o cliente seja usado:

```
public class Client {
    private Service service;

    // The dependency is injected through a setter method.
    public void setService(Service service) {
        if (service == null) {
            throw new IllegalArgumentException("service must not be null");
        }
        this.service = service;
    }
}
```


5. injeção de interface: a dependência fornece um método injetor que injetará a dependência em qualquer cliente passado para ela. Os clientes devem implementar uma interface que exponha um método setter que aceite a dependência:

```
public interface ServiceSetter {
    public void setService(Service service);
}

public class Client implements ServiceSetter {
    private Service service;

    @Override
    public void setService(Service service) {
        if (service == null) {
            throw new IllegalArgumentException("service must not be null");
        }
        this.service = service;
    }
}

public class ServiceInjector {
	private Set<ServiceSetter> clients;

	public void inject(ServiceSetter client) {
		this.clients.add(client);
		client.setService(new ExampleService());
	}

	public void switch() {
		for (Client client : this.clients) {
			client.setService(new AnotherExampleService());
		}
	}
}

public class ExampleService implements Service {}

public class AnotherExampleService implements Service {}
```


## Vantagens X Desvantagens

### Benefits of using DI

1. Helps in Unit testing.
2. Boilerplate code is reduced, as initializing of dependencies is done by the injector component.
3. Extending the application becomes easier.
4. Helps to enable loose coupling, which is important in application programming.

### Disadvantages of DI

1. It’s a bit complex to learn, and if overused can lead to management issues and other problems.
2. Many compile time errors are pushed to run-time.
3. Dependency injection frameworks are implemented with reflection or dynamic programming. This can hinder use of IDE automation, such as “find references”, “show call hierarchy” and safe refactoring.


https://en.wikipedia.org/wiki/Dependency_injection