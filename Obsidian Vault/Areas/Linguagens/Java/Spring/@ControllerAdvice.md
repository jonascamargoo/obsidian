
## O que é?

Para implementar a classe responsável por gerenciar todas as exceções, utilizaremos a anotação `@ControllerAdvice`. Essa anotação pertence ao Spring Framework e é empregada para lidar com exceções lançadas em qualquer parte da aplicação, não se limitando apenas aos controllers.

Conforme a documentação oficial do Spring, `@ControllerAdvice` é uma especialização da anotação `@Component`, proporcionando a capacidade de manipular exceções em todo o aplicativo como um componente global.

Podemos conceber o `@ControllerAdvice` como uma barreira que intercepta todas as exceções ocorridas dentro de um método/classe anotado com `@RequestMapping` antes de serem apresentadas ao usuário final. Podemos visualizar isso da seguinte forma

![[Pasted image 20240106184713.png]]


