---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-14'
---

## O que é?

O AWS Well-Architected Framework, ou simplesmente WAF, é um conjunto de práticas recomendadas para projetar e operar sistemas na nuvem AWS. Ele foi criado pela AWS com base na experiência de arquitetar soluções para uma ampla variedade de cenários e casos de uso. O AWS Well-Architected Framework ajuda você a entender os prós e os contras das decisões que você toma ao criar sistemas na AWS, e a aprender as melhores práticas de arquitetura para sistemas confiáveis, seguros, eficientes, econômicos e sustentáveis na nuvem.

## Por que usar?

Usar o AWS Well-Architected Framework traz vários benefícios, tais como:

- Aumentar a confiança e a capacidade de tomar decisões arquiteturais informadas;
- Melhorar a qualidade e a performance dos sistemas na nuvem;
- Reduzir os riscos e os custos associados aos sistemas na nuvem;
- Acelerar a inovação e a entrega de valor para os clientes;
- Alinhar os sistemas com as melhores práticas e os padrões da AWS;
- Preparar-se para o exame AWS Cloud Practitioner 😉

## Os seis pilares do WAF para a nuvem moderna

### Excelência Operacional

O pilar de excelência operacional se concentra na execução e no monitoramento de sistemas e na melhoria contínua de processos e procedimentos. Os principais tópicos deste pilar são:

- Automatizar as mudanças: usar processos automatizados para aplicar mudanças nos sistemas, reduzindo erros humanos, aumentando a velocidade e a consistência, e facilitando o rastreamento e a reversão de mudanças;

- Reagir a eventos: usar mecanismos de resposta a eventos para acionar ações automatizadas ou notificações quando ocorrem eventos significativos nos sistemas, como falhas, picos de demanda, alterações de configuração, etc;

- Definir padrões: usar padrões e políticas para estabelecer as expectativas e os requisitos de qualidade dos sistemas, e para facilitar a comunicação e a colaboração entre as equipes envolvidas no ciclo de vida dos sistemas;

- Antecipar falhas: usar técnicas de teste e simulação para identificar e eliminar pontos de falha nos sistemas, e para aumentar a resiliência e a tolerância a falhas dos sistemas;

- Aprender com a experiência: usar métricas e indicadores para monitorar o desempenho e a saúde dos sistemas, e para coletar e analisar dados sobre os eventos e as mudanças que ocorrem nos sistemas, gerando aprendizados e ações de melhoria.

### Segurança

O pilar de segurança se concentra na proteção de informações e sistemas, incluindo confidencialidade, integridade e disponibilidade de dados, gerenciamento de identidades e acessos, e detecção e resposta a eventos de segurança. Os principais tópicos deste pilar são:

- Implementar um forte controle de identidade: usar o princípio do menor privilégio para conceder apenas os acessos necessários aos recursos e operações dos sistemas, e usar mecanismos de autenticação e autorização robustos e seguros para validar as identidades e os acessos dos usuários e das aplicações;

- Proteger os dados em trânsito e em repouso: usar técnicas de criptografia e assinatura para garantir a confidencialidade e a integridade dos dados que são transmitidos ou armazenados nos sistemas, e usar mecanismos de gerenciamento de chaves seguros e confiáveis para proteger as chaves de criptografia;

- Aplicar a defesa em profundidade: usar múltiplas camadas de segurança para proteger os sistemas contra ataques, incluindo firewalls, grupos de segurança, listas de controle de acesso, detecção e prevenção de intrusão, isolamento de rede, etc;

- Automatizar a segurança: usar processos automatizados para aplicar as políticas e os padrões de segurança nos sistemas, e para detectar e responder a eventos de segurança, como tentativas de invasão, violações de dados, vulnerabilidades, etc;

- Preparar-se para incidentes de segurança: usar planos e procedimentos para lidar com incidentes de segurança, incluindo comunicação, investigação, recuperação, análise e ações corretivas.


### Confiabilidade

O pilar de confiabilidade se concentra na capacidade dos sistemas de executar as funções pretendidas e de se recuperar rapidamente de falhas, atendendo às demandas de mudança e crescimento. Os principais tópicos deste pilar são:

- Testar a recuperação: usar técnicas de teste e simulação para verificar a capacidade dos sistemas de se recuperar de falhas, e para medir os tempos e os impactos de recuperação;

- Gerenciar alterações: usar processos de gerenciamento de mudanças para controlar e monitorar as alterações nos sistemas, e para avaliar os riscos e os benefícios das alterações;

- Lidar com a demanda: usar técnicas de escalabilidade e elasticidade para ajustar a capacidade dos sistemas de acordo com a demanda, e para evitar a degradação ou a indisponibilidade dos sistemas;

- Distribuir os recursos: usar técnicas de distribuição e balanceamento de carga para distribuir os recursos dos sistemas entre múltiplas zonas de disponibilidade e regiões, e para aumentar a disponibilidade e a performance dos sistemas;

- Monitorar e alertar: usar métricas e indicadores para monitorar o desempenho e a saúde dos sistemas, e para gerar alertas quando ocorrem anomalias ou falhas nos sistemas.

### Eficiência de Performance

O pilar de eficiência de performance se concentra na alocação eficaz e otimizada de recursos de TI e computação, incluindo seleção, provisionamento, monitoramento e ajuste de recursos. Os principais tópicos deste pilar são:

- Selecionar os recursos certos: usar os recursos de TI e computação que melhor atendem aos requisitos funcionais e não funcionais dos sistemas, considerando fatores como tipo, tamanho, capacidade, performance, custo, etc;

- Provisionar os recursos de forma eficiente: usar técnicas de provisionamento e configuração de recursos para alocar os recursos de forma rápida e consistente, e para evitar o desperdício ou a subutilização de recursos;

- Monitorar e avaliar os recursos: usar métricas e indicadores para monitorar o desempenho e a utilização dos recursos, e para avaliar se os recursos estão atendendo às expectativas e aos objetivos dos sistemas;

- Ajustar os recursos de forma dinâmica: usar técnicas de ajuste e otimização de recursos para adaptar os recursos às mudanças nas condições e nas demandas dos sistemas, e para melhorar a performance e a eficiência dos recursos.

### Otimização de Custos

O pilar de otimização de custos se concentra na obtenção do melhor retorno sobre o investimento em recursos de TI e computação, incluindo análise, medição, previsão e controle de custos. Os principais tópicos deste pilar são:

- Analisar e atribuir os custos: usar ferramentas e métodos para analisar e atribuir os custos dos recursos de TI e computação, e para entender os fatores que influenciam os custos, como uso, performance, qualidade, etc;

- Medir e reportar os custos: usar ferramentas e métodos para medir e reportar os custos dos recursos de TI e computação, e para comparar os custos com os orçamentos e os objetivos dos sistemas;

- Prever e planejar os custos: usar ferramentas e métodos para prever e planejar os custos dos recursos de TI e computação, e para estimar os cenários e as tendências de custos;

- Controlar e otimizar os custos: usar ferramentas e métodos para controlar e otimizar os custos dos recursos de TI e computação, e para aproveitar as oportunidades de redução de custos, como descontos, reservas, modelos de consumo, etc.

### Sustentabilidade

Já ouviram falar de Green Software? Não!? Então dá uma olhadinha no nosso curso ["Green Software Development"](https://web.dio.me/play?search=Green%20Software%20Development), pois ele tem uma sinergia incrível com esse pilar. Especificamente, o pilar de sustentabilidade se concentra na redução do impacto ambiental dos sistemas na nuvem, incluindo consumo de energia, emissão de carbono, uso de materiais e descarte de resíduos. Os principais tópicos deste pilar são:

- Medir o impacto ambiental: usar ferramentas e métodos para medir o impacto ambiental dos recursos de TI e computação, e para entender os fatores que influenciam o impacto, como localização, fonte de energia, eficiência energética, etc;

- Reportar o impacto ambiental: usar ferramentas e métodos para reportar o impacto ambiental dos recursos de TI e computação, e para comparar o impacto com as metas e os objetivos de sustentabilidade dos sistemas;

- Reduzir o impacto ambiental: usar ferramentas e métodos para reduzir o impacto ambiental dos recursos de TI e computação, e para aproveitar as oportunidades de melhoria de sustentabilidade, como migração para regiões mais verdes, otimização de recursos, uso de serviços gerenciados, etc;

- Compensar o impacto ambiental: usar ferramentas e métodos para compensar o impacto ambiental dos recursos de TI e computação, e para apoiar iniciativas de sustentabilidade, como projetos de carbono neutro, programas de reciclagem, doações para ONGs ambientais, etc.
### Síntese dos seis pilares

- **Excelência operacional:** se concentra na execução e no monitoramento de sistemas e na melhoria contínua de processos e procedimentos;
- **Segurança:** se concentra na proteção de informações e sistemas, incluindo confidencialidade, integridade e disponibilidade de dados, gerenciamento de identidades e acessos, e detecção e resposta a eventos de segurança;
- **Confiabilidade:** se concentra na capacidade dos sistemas de executar as funções pretendidas e de se recuperar rapidamente de falhas, atendendo às demandas de mudança e crescimento;
- **Eficiência de performance:** se concentra na alocação eficaz e otimizada de recursos de TI e computação, incluindo seleção, provisionamento, monitoramento e ajuste de recursos;
- **Otimização de custos:** se concentra na obtenção do melhor retorno sobre o investimento em recursos de TI e computação, incluindo análise, medição, previsão e controle de custos;
- **Sustentabilidade:** se concentra na redução do impacto ambiental dos sistemas na nuvem, incluindo consumo de energia, emissão de carbono, uso de materiais e descarte de resíduos.


## Reflexões sobre os seis pilares

### Escalabilidade vs Elasticidade - como os pilares se diferenciam

Um exemplo de como os pilares se diferenciam é a distinção entre escalabilidade e elasticidade. Escalabilidade é a capacidade de um sistema de lidar com o aumento ou a diminuição da demanda, mantendo a performance e a disponibilidade. Elasticidade é a capacidade de um sistema de ajustar a capacidade dos recursos de forma dinâmica e automática, de acordo com a demanda. Escalabilidade está relacionada ao pilar de confiabilidade, pois afeta a capacidade do sistema de executar as funções pretendidas e de se recuperar de falhas. Elasticidade está relacionada ao pilar de eficiência de performance, pois afeta a alocação eficaz e otimizada de recursos de TI e computação. Portanto, para projetar e operar sistemas confiáveis e eficientes na nuvem, é preciso considerar tanto a escalabilidade quanto a elasticidade dos sistemas, e aplicar as melhores práticas de cada pilar.


### Segurança vs Confiabilidade - pilares se complementando

Um exemplo de como os pilares se complementam é a relação entre segurança e confiabilidade. Segurança é a proteção de informações e sistemas, incluindo confidencialidade, integridade e disponibilidade de dados, gerenciamento de identidades e acessos, e detecção e resposta a eventos de segurança. Confiabilidade é a capacidade dos sistemas de executar as funções pretendidas e de se recuperar rapidamente de falhas, atendendo às demandas de mudança e crescimento. Segurança e confiabilidade estão intimamente ligadas, pois a segurança afeta a confiabilidade e vice-versa. Por exemplo, um ataque de negação de serviço pode comprometer a disponibilidade e a performance de um sistema, afetando a sua confiabilidade. Por outro lado, uma falha de um sistema pode expor dados sensíveis ou permitir acessos não autorizados, afetando a sua segurança. Portanto, para projetar e operar sistemas seguros e confiáveis na nuvem, é preciso considerar a interação entre os pilares de segurança e confiabilidade, e aplicar as melhores práticas de ambos.

### Otimização de Custos vs Sustentabilidade - pilares se complementando

Outro exemplo de como os pilares se complementam é a relação entre otimização de custos e sustentabilidade. Otimização de custos é a obtenção do melhor retorno sobre o investimento em recursos de TI e computação, incluindo análise, medição, previsão e controle de custos. Sustentabilidade é a redução do impacto ambiental dos sistemas na nuvem, incluindo consumo de energia, emissão de carbono, uso de materiais e descarte de resíduos. Otimização de custos e sustentabilidade estão alinhadas, pois a otimização de custos implica na redução do consumo de recursos de TI e computação, o que por sua vez implica na redução do impacto ambiental dos sistemas na nuvem. Por exemplo, ao usar serviços gerenciados, você pode reduzir os custos de operação e manutenção dos recursos, e também reduzir o consumo de energia e a emissão de carbono dos recursos. Por outro lado, ao usar regiões mais verdes, você pode reduzir o impacto ambiental dos recursos, e também aproveitar os descontos e os incentivos oferecidos pela AWS. Portanto, para projetar e operar sistemas econômicos e sustentáveis na nuvem, é preciso considerar a sinergia entre os pilares de otimização de custos e sustentabilidade, e aplicar as melhores práticas de ambos.