## Infraestrutura global

### Região

Uma região é uma área geográfica onde a AWS possui um conjunto de data centers, que são locais onde os servidores, redes, armazenamentos e outros recursos de TI são armazenados e operados. 
### Zona

Uma zona de disponibilidade é uma parte (local físico) isolado de uma região, onde a AWS possui um ou mais data centers, que são conectados por redes de alta velocidade e baixa latência, garantindo alta disponibilidade e confiabilidade para os serviços em execução. A AWS possui atualmente (2023 - 24) [33 regiões e 105 zonas de disponibilidade ao redor do mundo](https://aws.amazon.com/pt/about-aws/global-infrastructure), e está constantemente expandindo a sua presença global. 
## Garantindo alta disponibilidade

A alta disponibilidade significa que os seus recursos de TI estão sempre acessíveis e operacionais, sem interrupções ou falhas. A nuvem AWS garante a alta disponibilidade dos seus recursos de TI por meio de vários mecanismos, como a redundância, o balanceamento de carga, o backup e a recuperação.
### Redundância

A redundância significa que os seus recursos de TI são replicados em várias zonas de disponibilidade dentro de uma região, ou em várias regiões, para evitar que um único ponto de falha afete o seu serviço.

### Load Balance

O balanceamento de carga significa que os seus recursos de TI são distribuídos entre várias instâncias, ou seja, cópias virtuais dos seus servidores, para evitar que uma instância sobrecarregada comprometa o seu desempenho. Imagine um restaurante lotado: garçons atendem as mesas, mas se apenas um garçom atender todas as mesas, o serviço ficará lento e os clientes ficarão insatisfeitos. O balanceamento de carga na AWS é como ter vários garçons experientes trabalhando juntos, garantindo um atendimento rápido e eficiente para todos os clientes, mesmo em horários de pico.
### No contexto AWS

No contexto da AWS, o balanceamento de carga distribui o tráfego de forma inteligente entre **diversas instâncias**, sejam elas servidores físicos ou virtuais. Isso significa que, em vez de todas as requisições caírem sobre uma única instância, elas são distribuídas entre várias, **evitando sobrecarga e gargalos**.

Benefícios do Balanceamento de Carga:

- **Maior disponibilidade:** Se uma instância falhar, as outras continuarão operando, garantindo que seus serviços fiquem online.
- **Melhor desempenho:** Distribui o tráfego, reduzindo o tempo de resposta e melhorando a experiência do usuário.
- **Escalabilidade:** Permite adicionar ou remover instâncias facilmente para atender às mudanças na demanda.
- **Maior resiliência:** Torna seus serviços mais resistentes a falhas e indisponibilidades.
- **Custos otimizados:** Evita o desperdício de recursos, pois as instâncias só são utilizadas quando necessário.

**Tipos de Balanceadores de Carga na AWS:**

A AWS oferece diferentes tipos de balanceadores de carga para atender às suas necessidades específicas:

- **Application Load Balancer (ALB):** Ideal para aplicações modernas baseadas em HTTP e HTTPS.
- **Network Load Balancer (NLB):** Projetado para alto desempenho e baixa latência, ideal para aplicações stateless e tráfego UDP.
- **Classic Load Balancer (CLB):** Uma opção mais antiga, ainda suportada, mas com menos recursos que os balanceadores mais novos.

### Backup

O backup significa que os seus dados são copiados e armazenados em locais seguros, para evitar que uma perda ou corrupção de dados prejudique o seu negócio
### Recuperação

 A recuperação significa que os seus recursos de TI são restaurados rapidamente em caso de uma falha ou desastre, para evitar que uma interrupção prolongada afete o seu serviço

## Elasticidade

A elasticidade significa que os seus recursos de TI podem se adaptar às mudanças na demanda, aumentando ou diminuindo a capacidade conforme a necessidade. A nuvem AWS permite que você faça a elasticidade dos seus recursos de TI de forma manual ou automática, de acordo com as métricas de desempenho que você definir. Assim, a nuvem AWS te permite atender às variações na demanda, sem comprometer a qualidade ou o custo do seu serviço.
## Agilidade

A agilidade significa que os seus recursos de TI podem ser lançados, modificados ou encerrados em questão de minutos, sem depender de processos complexos ou demorados. A nuvem AWS permite que você faça a agilidade dos seus recursos de TI por meio de uma interface web, uma linha de comando ou uma API, que são formas de interagir com os serviços da AWS. Assim, a nuvem AWS te permite inovar, experimentar e iterar rapidamente, sem perder tempo ou dinheiro.



## Sintetizando os conceitos

Imagine que você tem um aplicativo de delivery de comida, que conecta restaurantes e clientes. Você quer que o seu aplicativo seja sempre disponível, elástico e ágil, para oferecer o melhor serviço possível. Mas como você pode garantir isso? Bom, se você usar a nuvem AWS, você pode contar com os seguintes benefícios:

- Alta disponibilidade: Você pode replicar o seu aplicativo em várias zonas de disponibilidade ou regiões da AWS, para evitar que uma falha em um data center afete o seu serviço. Você pode distribuir o seu aplicativo entre várias instâncias da AWS, para evitar que uma instância sobrecarregada comprometa o seu desempenho. Você pode copiar e armazenar os seus dados em serviços da AWS, como o S3 (Simple Storage Service) ou o RDS (Relational Database Service), para evitar que uma perda ou corrupção de dados prejudique o seu negócio. Você pode restaurar o seu aplicativo rapidamente em caso de uma falha ou desastre, usando serviços da AWS, como o CloudFormation ou o CloudEndure, para evitar que uma interrupção prolongada afete o seu serviço.

- Elasticidade: Você pode adaptar o seu aplicativo às mudanças na demanda, aumentando ou diminuindo a capacidade conforme a necessidade. Você pode fazer isso de forma manual, usando serviços da AWS, como o EC2 (Elastic Compute Cloud) ou o Lambda, para lançar ou encerrar instâncias do seu aplicativo. Ou você pode fazer isso de forma automática, usando serviços da AWS, como o Auto Scaling ou o Fargate, para escalar o seu aplicativo de acordo com as métricas de desempenho que você definir.

- Agilidade: Você pode lançar, modificar ou encerrar o seu aplicativo em questão de minutos, sem depender de processos complexos ou demorados. Você pode fazer isso por meio de uma interface web, usando o Console da AWS, que é uma página na internet onde você pode acessar e gerenciar os serviços da AWS. Ou você pode fazer isso por meio de uma linha de comando, usando o AWS CLI (Command Line Interface), que é um programa que você pode instalar no seu computador e digitar comandos para interagir com os serviços da AWS. Ou você pode fazer isso por meio de uma API, usando o AWS SDK, que é um conjunto de bibliotecas que você pode usar em diferentes linguagens de programação para integrar o seu aplicativo com os serviços da AWS.