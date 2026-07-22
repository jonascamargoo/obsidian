---
tipo: conceito
area: Arquitetura e Eng. Software
tags:
- dev/arquitetura
criada: '2024-10-14'
---

## O que é?

	_Mensageria é um conceito que define que sistemas distribuídos, possam se comunicar por meio de troca de mensagens (evento), sendo estas mensagens “gerenciadas” por um Message Broker (servidor/módulo de mensagens).

### O que é um message broker?

	Um nada mais é que um servidor de mensagens, responsável por garantir que a mensagem seja enfileirada e armazenada em disco (opcional), garantindo que ela fique lá enquanto necessário até que alguém (consumidor) a retire de lá. Basicamente uma caixa de correios pública. É uma infraestrutura que permite a comunicação assíncrona entre diferentes sistemas, aplicativos ou componentes distribuídos, por meio do uso de mensagens.

### Representação

Aplicação A e B desacopladas, com a lógica inteiramente na A e a integração com a API rest na B:

![[Pasted image 20230725092943.png]]

Podemos observar alguns conceitos: 
*  _Exchange_ -> As trocas são responsáveis por receber as mensagens dos produtores e encaminhá-las para as filas corretas, seguindo determinadas regras de roteamento. Existem vários tipos de trocas com diferentes algoritmos de roteamento, como fanout, direct, topic e headers;

* _Queues_ -> recebe mensagem do Producer e armazena, até a retirada por um Consumer;

*  _Producers_ -> aplicação que envia mensagem para a queue do message broker;

*  _Consumers_ -> aplicação que retirará a mensagem

*  _Bindings_ -> regras ou associações que definem a relação entre as filas (queues) e as trocas (exchanges)

*  AMQP -> _Advanced Message Queuing Protocol_, é um protocolo especifico para comunicação baseada em mensagens (é o mais implementado por message brokers)

### Vantagens da aplicação neste exemplo

* A **Aplicação A** não precisar se preocupar se a **Aplicação B** vai estar disponível no momento em que ela enviar o evento;

*  Os eventos gerados podem ser persistidos em disco pelo Message Broker. Isso é opcional e você define no momento da criação da _queue_, mas com certeza você vai configurar para que isso aconteça, afinal você não quer que nenhuma mensagem seja perdida caso o Message Broker seja reiniciado;

* Caso o _consumer_ não consiga confirmar a leitura da mensagem (ack) a mesma continuará enfileirada, até que em outro momento ele consiga confirmar a leitura;

*  A única responsabilidade da **Aplicação A** é comunicar que houve um evento e que mesmo deve ser integrado quando possível. Ela nem sabe como a B foi desenvolvida]


## O que é uma mensagem?

No contexto do Message Broker, a "mensagem" é o pacote de dados que contém informações que precisam ser transmitidas de um componente do sistema para outro. Essas mensagens são unidades fundamentais de comunicação assíncrona entre diferentes aplicativos ou sistemas distribuídos.

A mensagem é composta por dois elementos principais:

### **Label (Etiqueta)**

	O "label" é um atributo ou metadado que é anexado à mensagem para identificar o tipo ou a categoria da mensagem. Ele é usado como uma marca ou rótulo para fins de roteamento, filtragem ou classificação de mensagens dentro do Message Broker. O label é útil quando se deseja categorizar as mensagens de acordo com seu conteúdo ou propósito, permitindo que o Message Broker encaminhe essas mensagens para filas específicas ou consumidores interessados apenas em um determinado tipo de mensagem.
	
	Por exemplo, imagine um sistema de e-commerce que utiliza um Message Broker para tratar pedidos, atualizações de estoque e informações de envio. As mensagens relacionadas a esses três tipos diferentes de eventos podem ser rotuladas com etiquetas como "Pedido", "Estoque" e "Envio", respectivamente. Com base nessas etiquetas, o Message Broker pode encaminhar cada mensagem para a fila correta, onde os consumidores apropriados (processadores) estarão esperando para tratá-las adequadamente.


### **Payload**

	O "payload" é o conteúdo real da mensagem, ou seja, os dados que estão sendo transportados e transmitidos entre os componentes do sistema. O payload é a informação significativa que os produtores enviam e os consumidores processam.
	
	Por exemplo, se estamos lidando com mensagens em formato JSON, o payload será a estrutura JSON contendo todas as informações relevantes da mensagem. Se a mensagem estiver transportando uma imagem ou um arquivo, o payload conterá os dados binários desses arquivos.

Em resumo, o label é um metadado que auxilia na classificação e roteamento de mensagens, enquanto o payload contém os dados reais que precisam ser transmitidos entre os componentes do sistema. Juntos, eles formam a mensagem completa, que é enviada através do Message Broker para permitir a comunicação assíncrona e desacoplada entre os diferentes componentes de um sistema distribuído:

![[Pasted image 20230725100732.png]]


**A seta cortada representa a mensagem**.