---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-14'
---

### Opções de Compra de Computação na AWS

A AWS oferece várias opções de compra de computação para atender a diferentes necessidades de negócios e técnicas, incluindo instâncias sob demanda, instâncias reservadas, Spot Instances, Savings Plans, hosts dedicados, instâncias dedicadas e reserva de capacidade.

- **Instâncias sob demanda** oferecem a maior flexibilidade, permitindo que você pague pelas capacidades computacionais por hora ou segundo, com a opção de parar a instância e não incorrer em custos quando ela não estiver em uso. Esta opção é ideal para aplicações com demandas variáveis ou imprevisíveis, onde o compromisso a longo prazo não é possível.
- **Instâncias reservadas** proporcionam um desconto significativo (até 75%) em comparação com os preços das instâncias sob demanda, em troca de um compromisso de uso por um período de um ou três anos. Este modelo é adequado para aplicações com estado estável ou previsível.
- **Spot Instances** permitem que você aproveite a capacidade computacional não utilizada na AWS com descontos substanciais em relação às instâncias sob demanda. O preço das Spot Instances varia de acordo com a oferta e a demanda e é ideal para tarefas que podem ser interrompidas, como processamento em batch de grande volume.
- **Savings Plans** é um modelo de compromisso flexível que oferece descontos significativos em relação à utilização sob demanda, em troca de um compromisso de uso de um ou três anos de uma quantidade específica de capacidade computacional, medido em dólares por hora.
- **Hosts dedicados** são servidores físicos dedicados para o seu uso, úteis para atender a requisitos regulatórios que não permitem o compartilhamento de recursos.
- **Instâncias dedicadas** são instâncias que rodam em hardware dedicado a um único cliente, mas diferem dos hosts dedicados por serem mais flexíveis quanto à configuração.
- **Reserva de capacidade** garante a disponibilidade da capacidade de computação quando você precisa, ideal para aplicações críticas que exigem capacidade reservada para garantir a disponibilidade.

Comparar as opções de compra de computação na AWS pode ser semelhante a escolher entre diferentes planos de celular. Instâncias sob demanda são como planos pré-pagos, onde você paga exatamente pelo que usa, sem compromissos. Instâncias reservadas são semelhantes a contratos de longo prazo que oferecem melhores tarifas em troca de um compromisso de uso. Spot Instances são como comprar minutos extras a uma taxa mais baixa quando a rede está menos ocupada. Savings Plans são como planos familiares onde o compromisso não é com o uso individual, mas com o total gasto pela família, oferecendo flexibilidade em quem usa os recursos dentro de um orçamento fixo. Hosts dedicados e instâncias dedicadas são como ter um plano exclusivo que garante que ninguém mais possa usar seus recursos específicos, com hosts dedicados oferecendo o nível mais alto de exclusividade e personalização.

### Cobranças de Transferência de Dados

As cobranças de transferência de dados na AWS são calculadas com base na quantidade de dados transferidos para fora da AWS para a internet ou entre regiões AWS. A transferência de dados para dentro da AWS é geralmente gratuita, enquanto a saída de dados é cobrada com base na quantidade total de dados transferidos.

- **Dentro da mesma região**, a transferência de dados entre serviços AWS é geralmente gratuita ou incide um custo mínimo quando os serviços estão em zonas de disponibilidade diferentes.
- **Entre regiões**, a transferência de dados é cobrada por GB transferido, e os custos podem variar dependendo das regiões de origem e destino.
- A transferência de dados **para a internet** inclui custos que aumentam com o volume de dados transferidos. A AWS oferece uma quantidade mínima de dados que podem ser transferidos gratuitamente, conhecida como nível de uso gratuito.

Pense nas cobranças de transferência de dados como uma viagem de carro onde, geralmente, não há custo para entrar em uma cidade (transferir dados para a AWS), mas há pedágios ao sair da cidade ou ao viajar entre cidades (transferir dados para fora da AWS ou entre regiões). Viajar dentro da mesma cidade (transferência de dados na mesma região) pode ser gratuito ou ter um custo mínimo, dependendo da rota (serviços AWS utilizados).

### Opções e Níveis de Armazenamento

A AWS oferece uma ampla variedade de serviços de armazenamento para atender a diferentes necessidades de armazenamento, incluindo Amazon S3 para armazenamento de objetos, Amazon EBS para armazenamento de blocos, e Amazon Glacier para arquivamento de longo prazo. Cada serviço tem várias opções de preço baseadas no volume de dados armazenados, na frequência de acesso aos dados e na durabilidade e disponibilidade dos dados.

- **Amazon S3** oferece diferentes classes de armazenamento, como S3 Standard para acesso frequente, S3 Intelligent-Tiering para acesso variável, S3 Standard-IA para acesso menos frequente, e S3 One Zone-IA para dados que não exigem múltiplas zonas de disponibilidade.
- **Amazon EBS** oferece volumes SSD e HDD, adequados para cargas de trabalho de alta performance e armazenamento econômico, respectivamente. Os preços variam com base no tamanho do volume, no desempenho (IOPS) e no tipo de volume.
- **Amazon Glacier** é uma solução de baixo custo para arquivamento e backup de longo prazo, com várias opções de recuperação de dados que variam em termos de tempo de recuperação e custo.

Escolher entre as opções e níveis de armazenamento na AWS é como selecionar entre diferentes opções de armazenamento para uma casa. Amazon S3 é como ter um armário grande e acessível para itens de uso diário, com diferentes seções (classes de armazenamento) para itens que você usa com frequências variadas. Amazon EBS é como ter uma garagem para armazenamento de veículos (dados de blocos) que você precisa acessar rapidamente e com frequência, com diferentes tamanhos de garagem (volumes) e opções de estacionamento (SSD vs. HDD) baseadas em suas necessidades de performance. Amazon Glacier é como ter um depósito fora da cidade para itens que você raramente precisa, mas quer manter seguros a longo prazo, com a opção de escolher quão rápido você pode trazê-los de volta quando necessário.

### Conclusão

Este conteúdo educacional apresenta uma visão geral sobre o modelo de preços da AWS, crucial para qualquer pessoa que aspire a se tornar um(a) AWS Certified Cloud Practitioner. Ao dominar esses conceitos, você estará mais preparado(a) para tomar decisões sobre a otimização de custos na AWS, garantindo que você possa projetar e operar sistemas econômicos sem comprometer a eficiência ou a escalabilidade.