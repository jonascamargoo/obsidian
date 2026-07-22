# O que é?

Event Driven Architecture (EDA) é um design pattern que propoe uma abordagem assíncrona para a comunicação entre serviços desacoplados, sendo muito comum em aplicações que seguem a abordagem de microserviços.

Essa arquitetura utiliza eventos para acionamento e comunicação entre esses serviço.

> [!important]  
> Um evento é uma mudança ou uma atualização no estado, como um item adicionado a um carrinho de compras em um site de comércio eletrônico. Eventos podem conter o estado (o item comprado, o preço ou um endereço de entrega) ou podem ser identificadores (uma notificação de que um pedido foi despachado, por exemplo).  

As arquiteturas por eventos tem 3 componentes fundamentais:

1. ==**Produtores (ou Publicadores)**====:== São as entidades ou processos responsáveis por gerar e emitir eventos. Cada evento representa um estado ou uma mudança significativa no sistema. Os produtores publicam esses eventos no roteador de eventos sem se preocupar com os detalhes de quem irá consumi-los ou como serão processados, promovendo assim um baixo acoplamento e uma alta coesão entre os componentes do sistema.
2. ==**Roteadores (ou Brokers, Barramentos de Eventos)**====:== O roteador atua como um intermediário central, responsável por receber eventos dos produtores e encaminhá-los aos consumidores interessados. Ele gerencia o tráfego de eventos, garantindo que sejam entregues de forma confiável e eficiente. Além disso, o roteador pode implementar mecanismos de filtragem, transformação e agregação de eventos, bem como gerenciar tópicos ou filas para organizar a distribuição dos eventos.
3. ==**Consumidores (ou Assinantes)**====:== São os componentes que recebem e processam os eventos. Cada consumidor se inscreve para eventos específicos de seu interesse por meio do roteador. Quando um evento relevante é publicado, o roteador notifica o consumidor correspondente, que então ativa sua lógica de processamento. Os consumidores podem reagir aos eventos executando tarefas, atualizando estados, ou até mesmo produzindo novos eventos, contribuindo para a natureza reativa e escalável da arquitetura.

# Como funciona?

Nessa abordagem, para que os serviços independentes de um mesmo sistema comuniquem-se entre si, são utilizados eventos, como um canal de comunicação ==assíncrono== entre eles.

[![](https://www.notion.so)](https://www.notion.so)

## Produção de Eventos

Serviços que produzem novos eventos, que irão acionar a execução dos demais, são os chamados produtores, e eles serão responsáveis por publicar esses eventos nos chamados Routers/Brokers no canal correto. O canal correto, seria um dos diversos canais que podem existir dentro de uma aplicação baseada nesse estilo, que corresponde ao canal usado para notificar a ocorrência de eventos daquele tipo. Esses “canais” são chamados de _**tópicos**_**.**

_Exemplo: um e-commerce pode ter o tópico de novos pedidos, e também o tópico de pedidos cancelados._

Depois de publicar esse evento no _tópico_, o produtor não irá se preocupar com mais nada, ele não precisa esperar o consumidor processar esse evento, e inclusive o consumidor pode estar fora do ar e está tudo bem na visão do produtor.

## Armazenamento e notificação desses eventos

O Broker por sua vez, irá armazenar esse evento, e notificar todos consumidores interessados naquele canal (que se inscreveram para receber notificações quando novos eventos fossem criados).

**👉** Aqui a implementação pode variar, mas muitas vezes o Broker guarda esses eventos em uma fila, essa fila armazena os eventos até os consumidores tenham consumido, dessa maneira, caso eles estejam fora do ar, os eventos não serão perdidos e poderão ser processados depois (async 😃)

## Consumo dos eventos

Por fim, o consumidor irá consumir esses eventos. Ele pode tanto consumir de uma fila, quando existir, ou consumir esses eventos diretamente do tópico. Mas nesse caso, caso o consumidor não esteja em pé quando um evento for postado no tópico, ele irá perder esse evento.

Imagine o tópico como um túnel, onde apenas a pessoa da esquerda pode falar, e a pessoa da direita só pode ouvir. Caso a pessoa da direita tenha ido pegar uma água, ela pode perder uma mensagem que a pessoa da esquerda gritou no túnel

[![](https://wasaki.com.br/wp-content/uploads/2023/03/tunel-12bis-o-maior-do-brasil-curiosidades.jpg)](https://wasaki.com.br/wp-content/uploads/2023/03/tunel-12bis-o-maior-do-brasil-curiosidades.jpg)

# Tecnologias populares

## Kakfa

O Kafka é um sistema pub-sub (publicação-assinatura), ==**mas com características e capacidades que vão além do padrão pub-sub básico.**==

Cada servidor individual no cluster Kafka é um broker.

Então eles servem como ponto de conexão para os produtores (publishers) enviarem mensagens e para os consumidores (subscribers) retirarem mensagens.

No Kafka os brokers também são responsáveis por armazenar os dados de forma segura e replicá-los em múltiplos nodos para garantir a resiliência e alta disponibilidade do sistema.

> O Kafka armazena as mensagens de forma durável em disco e permite que as mensagens sejam retidas por um período configurável, independentemente de terem sido consumidas. Isso permite que os consumidores leiam e processem mensagens atrasadas e fornece um buffer de dados para recuperação e análise.

## Simple Queue Service (SQS)

O termo "broker" é comumente associado a sistemas como o Kafka ou RabbitMQ.

O SQS não pode ser chamado de um serviço pub-sub como os demais, pois as mensagens são enviadas para uma fila e depois ==**retiradas**== por consumidores, uma vez consumidas as mensagens saem da fila. Normalmente, cada mensagem é processada por apenas um consumidor.

Em um sistema pub-sub, mensagens são publicadas em tópicos e _**entregues**_ a múltiplos assinantes que têm interesse nesse tópico, potencialmente permitindo que a mesma mensagem seja processada por múltiplos consumidores.

Mas devido a característica de atuar como um intermediário confiável entre produtores e consumidores de uma _**fila**_, podemos chamar o SQS de Broker também.

Ele garante a entrega de mensagens e ==permite que produtores e consumidores sejam desacoplados==, significando que eles não precisam estar operacionais ou conectados ao mesmo tempo.

Assim como o Kakfa, o SQS é altamente escalável e gerenciado.

## Simple Notification Service (SNS)

o Amazon SNS também pode ser conceitualmente considerado um broker, pois é um sistema pub-sub.

O SNS atua como um intermediário entre publicadores e assinantes, assumindo a responsabilidade de entregar mensagens publicadas para os assinantes corretos. Ele desacopla os produtores de mensagens dos consumidores, permitindo que eles operem independentemente.

- No SNS, os publicadores enviam mensagens para "tópicos". Um tópico é um ponto de acesso lógico e um canal de comunicação onde as mensagens são publicadas.
- Os assinantes podem se inscrever em tópicos para receber mensagens de seu interesse. O SNS suporta uma variedade de protocolos de assinantes, incluindo HTTP/S, e-mail, SMS e filas SQS, entre outros.

No Amazon SNS, se um consumidor estiver indisponível ou não operando no momento em que uma mensagem é entregue, a mensagem poderá ser perdida dependendo do tipo de assinante (HTTP, SMTP, SMS, SQS) e da configuração de entrega

1. **Assinantes HTTP/S**:
    - Para assinantes HTTP/S, o SNS tenta entregar a mensagem imediatamente. Se o assinante estiver indisponível ou se a entrega falhar (por exemplo, devido a erros do servidor), o SNS tentará entregar a mensagem várias vezes, seguindo uma política de nova tentativa definida pelo usuário.
    - Se todas as tentativas de entrega falharem, a mensagem pode ser perdida a menos que você tenha configurado um DLQ (Dead Letter Queue) para capturar mensagens que não podem ser entregues.
2. **Assinantes de E-mail/SMS**:
    - Para assinantes de e-mail ou SMS, o SNS envia a mensagem uma vez. Se o serviço de e-mail ou SMS não conseguir entregar a mensagem (por exemplo, devido a um endereço de e-mail inválido), a mensagem não será entregue, mas o SNS não tenta entregá-la novamente.
3. **Assinantes SQS (Filas do Amazon SQS)**:
    - Se você estiver usando uma fila do Amazon SQS como assinante, a mensagem é entregue à fila e permanecerá lá até ser processada pelo consumidor ou até o período de retenção da mensagem expirar. Isso significa que as mensagens não são perdidas se o consumidor estiver indisponível no momento da entrega; em vez disso, elas ficam na fila esperando o consumidor ficar disponível para processá-las.
    - Além disso, com o SQS, você pode configurar uma DLQ para capturar mensagens que falharam no processamento várias vezes.

# Quando usar?

## Microserviços

EDA aprimora a arquitetura de microservices, permitindo uma desacoplamento ainda maior entre serviços.

Em um sistema de ecommerce por exemplo, os microserviços como vendas e cobrança operam de forma independente, removendo o acoplamento temporal. Assim, mesmo que um serviço falhe (como o de cobrança), o sistema continua operando, processando novos pedidos e jogando-os para uma fila, para quando o serviço de cobrança estiver disponível novamente e consiga processar.

## Serviços de monitoramento

Em vez de conferir continuamente seus recursos, você pode usar uma arquitetura orientada por eventos para monitorar e receber alertas sobre anomalias, alterações e atualizações. Esses recursos podem incluir buckets de armazenamento, tabelas de banco de dados, funções sem servidor, nós de computação e muito mais.

  

## Para saber mais

> [!info] Arquitetura orientada por eventos  
> Uma arquitetura orientada por eventos usa eventos para acionamento e comunicação entre serviços.  
> [https://aws.amazon.com/pt/event-driven-architecture/#:~:text=An%20event-driven%20architecture%20uses,on%20an%20e-commerce%20website](https://aws.amazon.com/pt/event-driven-architecture/#:~:text=An%20event-driven%20architecture%20uses,on%20an%20e-commerce%20website)  

> [!info] 4 event-driven architecture use cases (with examples)  
> Discover four popular use cases for event-driven architecture, with examples of how it can be used it in action.  
> [https://ably.com/topic/event-driven-architecture-use-cases](https://ably.com/topic/event-driven-architecture-use-cases)  

> [!info] Event-driven Architecture (EDA) em uma arquitetura de Micro Serviços  
> Quando nos referimos a arquitetura de Micro Serviços e sua natureza de comunicação temos dois caminhos possíveis a considerar, comunicação…  
> [https://medium.com/@marcelomg21/event-driven-architecture-eda-em-uma-arquitetura-de-micro-serviços-1981614cdd45](https://medium.com/@marcelomg21/event-driven-architecture-eda-em-uma-arquitetura-de-micro-serviços-1981614cdd45)