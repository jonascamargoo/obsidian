---
tipo: conceito
area: Álgebra Linear
tags:
- matematica/algebra-linear
criada: '2024-10-14'
---

O conceito vem da ideia de um valor ter sempre, como resultado, a mesma potência. Como é o caso do 1^n=1. O conceito pode ser interpretado através de funções também: "Uma função é idempotente se aplicar ela 2 vezes retorna sempre o mesmo resultado que aplicar ela uma vez só" . Um exemplo é f(x) = x*1.

$$f(f(x))=f(x)$$

### Em computação?

	![[Pasted image 20240608204245.png]]
	

uma forma de pensar é que o nosso "x" pode ser todo o estado da nossa aplicação, e o nosso "f" uma operação da nossa API

	![[Pasted image 20240608204325.png]]

Uma forma de ver é que a idempotência representa que, se a gente fizer a mesma operação 2x com os mesmos argumentos, isso deveria ser *igual* a executar a operação uma vez só

	![[Pasted image 20240608204405.png]]

### Por que discutir isso?

Bom, o maior motivo pra fazer isso é que em sistemas distribuídos é muito difícil garantir que uma operação entre sistemas aconteça só uma vez. Por que? Porque sistemas distribuídos se comunicam pela rede, e a rede não é confiável

	![[Pasted image 20240608204439.png]]


Vamos considerar uma relação cliente-servidor simples - que, lembrando, é também um sistema distribuído. Se você considerar que pode haver requisições perdidas - e sempre há - um dos jeitos mais fáceis de lidar é pedir pro cliente retentar

	![[Pasted image 20240608204526.png]]

Mas e se a requisição foi recebida, e na verdade a *resposta do servidor* que foi perdida? Bom, você pode acabar criando algo duas vezes. E criar algo duas vezes pode acabar sendo bem ruim! Por exemplo, se você estiver criando uma transação financeira, o seu cliente pode acabar pagando duas vezes o que ele queria pagar! Então como podemos resolver isso? Bom, uma solução possível e bem comum é usar um ID de idempotência:

	![[Pasted image 20240608204545.png]]

A seguir, temos  simplesmente um dado aleatório enviado junto à requisição que o servidor usa pra validar se uma requisição é "a mesma" já tratada. Através dele, o servidor pode saber se está recebendo uma solicitação que já atualizou seu estado:

	![[Pasted image 20240608204618.png]]


Essa está longe de ser a única estratégia: Algumas operações, por exemplo, já são naturalmente idempotentes. Por exemplo, o método HTTP PUT, por sobrescrever uma entidade num ID específico, é idempotente: Sobrescrever 2x = sobrescrever 1x.

Usando ou não IDs de idempotência, a questão da idempotência é simples: Uma única requisição só deveria afetar o sistema uma vez. Isso é importante por exemplo usando filas de mensagens - a maioria das filas, pra atingir eficiência, não garante não repetir mensagens!