
Imagine que tenho vários microsserviços na minha arquitetura. Um usuário faz uma requisição para efetuar um pagamento. Essa requisição cai no microsserviço de pagamento, que por sua vez envia uma mensagem para o microsservice de Order e, enquanto isso, o Order faz uma requisição assíncrona para o serviço de pagamentos fazendo a cobrança, depois o payment processou o ppagamento e foi salvar no DB dele, mas o BD tava off. O sistema faz um retry, reenviando a mensagem, mas a cobrança foi duplicada. E agora, o cliente se ferrou, vai pagar duas vezes? Indepotência!

## Transações

Uma arquitetura distribuída depende de transações. Como garantir a transação nesse cenário?  Saga Patterntransação (requisição) que contemplam multiplos servicos, devem ser quebradas em microtransações.

![[Pasted image 20250910205937.png]]


Como um serviço não gerar latência no outro?

## Circuit Breaker

Healthcheck? Ele faz isso?