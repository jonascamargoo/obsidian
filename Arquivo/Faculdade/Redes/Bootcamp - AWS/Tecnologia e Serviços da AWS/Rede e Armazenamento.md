---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-14'
---

### Rede na AWS: Virtual Private Cloud (VPC)

Uma [Virtual Private Cloud (VPC)](https://aws.amazon.com/vpc/) oferece um ambiente isolado dentro da nuvem da AWS, onde você pode lançar recursos em uma rede virtual definida por você. Este ambiente é completamente isolado de outros usuários da AWS, o que proporciona um nível de segurança e controle similar ao que uma rede corporativa on-premises ofereceria, mas com a flexibilidade e a escala da nuvem.

#### Componentes Principais da VPC

Dentro de uma VPC, você tem a liberdade de configurar os componentes de rede de acordo com as necessidades específicas de suas aplicações. Os componentes incluem:

- **Sub-redes**: Divisões dentro de uma VPC que permitem segmentar recursos da AWS e alocá-los de forma lógica em diferentes blocos de IPs. Cada sub-rede reside totalmente dentro de uma única Zona de Disponibilidade (AZ) e pode ser pública ou privada, dependendo se tem uma rota para o gateway de internet.
- **Gateways de Internet (IGW)**: Atuam como o ponto de entrada para o tráfego da internet para as sub-redes públicas, permitindo que recursos dentro da VPC comuniquem-se com o mundo exterior. Para que uma instância em uma sub-rede privada acesse a internet, ela deve passar por um NAT Gateway localizado em uma sub-rede pública.
- **Tabelas de Rotas e Gateways NAT**: As tabelas de rotas direcionam o tráfego de rede dentro da VPC e para fora dela. Gateways NAT permitem que instâncias em sub-redes privadas acessem serviços na internet, sem permitir que a internet inicie uma conexão com essas instâncias.

#### Segurança em uma VPC

A AWS fornece várias camadas de segurança na VPC, incluindo:

- **Grupos de Segurança**: Funcionam como firewalls virtuais no nível da instância, permitindo especificar regras de tráfego de entrada e saída. Estas regras podem ser baseadas em IPs ou grupos de segurança, oferecendo flexibilidade na definição de políticas de acesso.
- **Listas de Controle de Acesso à Rede (NACLs)**: Atuam no nível da sub-rede, proporcionando uma camada adicional de segurança que pode ser usada para permitir ou bloquear o tráfego para uma ou mais sub-redes dentro de uma VPC.

#### Analogia

Pense em uma VPC como um condomínio privado. Dentro deste condomínio, sub-redes são casas individuais; IGWs são as portas principais para o mundo exterior; Grupos de Segurança são sistemas de segurança domésticos que controlam quem pode entrar ou sair de sua casa; e NACLs são os seguranças na entrada do condomínio, controlando quem pode entrar ou sair de cada rua.

### Amazon Route 53

[Amazon Route 53](https://aws.amazon.com/route53/) é um serviço de DNS web escalável e altamente disponível, desenhado para dar aos desenvolvedores e empresas uma maneira extremamente confiável e rentável de rotear os usuários finais para aplicações na internet. O Route 53 consegue efetivamente conectar as solicitações dos usuários a infraestruturas rodando dentro da AWS (como uma instância EC2 ou um balde S3) ou fora dela. Além disso, o Route 53 também oferece funcionalidades de registro de domínio, permitindo aos usuários comprar e gerenciar domínios.

- **Resolução de Nomes**: O Route 53 traduz nomes de domínio como [www.dio.me](http://www.dio.me/) em endereços IP numéricos como 192.0.2.1, que os computadores usam para conectar-se entre si. O Route 53 também responde a solicitações DNS para o domínio com o IP de um recurso, como uma instância EC2 ou um balde S3.
- **Políticas de Roteamento**: O serviço oferece várias políticas de roteamento, incluindo roteamento baseado em geolocalização, que permite responder a solicitações com base na localização geográfica do usuário final, e balanceamento de carga entre múltiplas regiões da AWS, aumentando a disponibilidade e reduzindo a latência.

Usar o Amazon Route 53 é como ter um guia de viagem extremamente eficiente para a internet. Assim como um guia sabe os melhores caminhos e como evitar o trânsito, o Route 53 direciona as solicitações dos usuários para sua aplicação pelo caminho mais eficiente possível.

### Serviços de Borda

Os serviços de borda da AWS, como [Amazon CloudFront](https://aws.amazon.com/cloudfront/) e [AWS Global Accelerator](https://aws.amazon.com/global-accelerator/), são projetados para melhorar a entrega de conteúdo e a experiência do usuário final, minimizando a latência e maximizando a performance.

#### Amazon CloudFront

O CloudFront é uma rede de entrega de conteúdo (CDN) que distribui conteúdo com segurança, como vídeos, dados, aplicações e APIs, para usuários em todo o mundo com baixa latência, altas velocidades de transferência, tudo dentro de um ambiente protegido. O serviço trabalha através de uma rede global de pontos de presença (PoPs), que cacheiam cópias do seu conteúdo em locais próximos aos usuários finais.

- **Distribuição de Conteúdo**: Ao armazenar cópias do conteúdo em cache em locais estratégicos, o CloudFront reduz a distância entre o usuário final e o conteúdo, resultando em melhor performance e menor latência.
- **Segurança**: O CloudFront integra-se com AWS Shield para proteção DDoS, além de oferecer a possibilidade de configurar HTTPS para criptografar dados em trânsito, protegendo as informações sensíveis dos usuários.

#### AWS Global Accelerator

O AWS Global Accelerator melhora a disponibilidade e performance das aplicações com tráfego global, direcionando os usuários para a rota de internet mais próxima e, a partir daí, para as aplicações rodando em múltiplas regiões da AWS. Ele usa a rede global da AWS para otimizar a rota do tráfego de usuários para suas aplicações.

- **Otimização de Rota**: Ao aproveitar a rede backbone global da AWS, o Global Accelerator minimiza os caminhos que o tráfego da internet precisa percorrer, melhorando a performance e a consistência da experiência do usuário.
- **Saúde da Aplicação**: O serviço monitora continuamente a saúde das suas aplicações e redireciona o tráfego para regiões saudáveis automaticamente, garantindo a disponibilidade da aplicação mesmo em caso de falhas.

#### Analogia

Imagine os serviços de borda como um sistema de entregas expresso global para o seu conteúdo digital. Se o CloudFront fosse um conjunto de armazéns locais espalhados pelo mundo, garantindo que os produtos cheguem rapidamente aos clientes locais, o Global Accelerator seria a rede de autoestradas que conecta esses armazéns, assegurando que os produtos se movam rapidamente entre regiões.

### Conectividade de Rede com a AWS

A AWS oferece soluções robustas de conectividade para integrar ambientes on-premises com a nuvem, como [AWS VPN](https://aws.amazon.com/vpn/) e [AWS Direct Connect](https://aws.amazon.com/directconnect/), cada uma atendendo a diferentes necessidades de desempenho, segurança e hibridização.

#### AWS VPN

A VPN da AWS permite a criação de uma conexão segura e privada entre a rede da sua empresa e sua VPC AWS, usando a internet como a ponte. Isso é ideal para casos de uso onde a segurança dos dados em trânsito é uma preocupação, mas onde a dedicatória de uma linha privada (como com o AWS Direct Connect) não se justifica pelo custo ou pela necessidade.

- **Conexão Segura**: Utilizando protocolos de segurança padrão da indústria, como SSL/TLS para a VPN baseada em software, a AWS VPN garante que os dados transmitidos entre sua rede e a AWS estejam seguros.
- **Flexibilidade**: Com a capacidade de configurar conexões VPN em minutos, a AWS VPN oferece uma solução flexível para a necessidade de acesso seguro e temporário à sua VPC.

#### AWS Direct Connect

O AWS Direct Connect permite estabelecer uma conexão de rede dedicada de sua infraestrutura on-premises para a AWS. Essa conexão direta pode reduzir custos de rede, aumentar a largura de banda e fornecer uma experiência de rede mais consistente do que conexões baseadas na internet.

- **Conexão de Alta Performance**: Ao oferecer uma conexão de rede dedicada, o AWS Direct Connect fornece uma experiência mais consistente e de alta performance para aplicações que exigem grandes volumes de dados ou uma baixa latência.
- **Redução de Custos**: Comparado ao uso de internet pública para conexão com a AWS, o Direct Connect pode reduzir significativamente os custos de transmissão de dados, especialmente para grandes volumes de tráfego.

#### Analogia

Se a AWS VPN é como uma ponte segura que permite a você acessar a sua casa de férias (VPC AWS) usando estradas públicas (internet), então o AWS Direct Connect é como ter uma linha ferroviária privada direto para sua casa de férias, oferecendo um caminho mais rápido, seguro e controlado.

### Armazenamento na AWS

O armazenamento na AWS é abrangente e diversificado, oferecendo soluções como armazenamento de objetos com [Amazon S3](https://aws.amazon.com/s3/), armazenamento em bloco com Amazon EBS, e serviços de arquivos como Amazon EFS e Amazon FSx. Cada serviço é otimizado para casos de uso específicos, desde armazenamento altamente disponível e globalmente acessível até soluções de armazenamento de alta performance para sistemas de arquivos.

#### Armazenamento de Objetos com Amazon S3

O S3 é um serviço de armazenamento de objetos projetado para armazenar e recuperar qualquer quantidade de dados de qualquer lugar na web. Ele oferece uma disponibilidade de 99,999999999% e está disponível em múltiplas classes de armazenamento que permitem otimizar custos e performance com base em como os dados são acessados.

- **Durabilidade e Disponibilidade**: O S3 armazena cópias dos dados em múltiplas instalações e em múltiplas Zonas de Disponibilidade dentro de uma região da AWS, garantindo alta durabilidade e disponibilidade.
- **Classes de Armazenamento**: Incluem S3 Standard para uso geral, S3 Intelligent-Tiering para dados com padrões de acesso variáveis, S3 Glacier e S3 Glacier Deep Archive para arquivamento de longo prazo com acesso raro.

#### Soluções de Armazenamento em Bloco: Amazon EBS

Os [volumes EBS](https://aws.amazon.com/ebs/) são projetados para uso com instâncias EC2, oferecendo armazenamento em bloco de alta performance que pode ser anexado como um disco rígido virtual. São ideais para bases de dados, sistemas de arquivos, ou qualquer aplicação que exija acesso a um armazenamento em bloco persistente.

- **Tipos de Volume**: Incluem volumes de SSD otimizados para performance (gp2 e io1/io2) para cargas de trabalho de I/O intensivo e volumes de HDD (st1 e sc1) otimizados para throughput, ideais para big data, data warehouses e cargas de trabalho de log.

#### Serviços de Arquivos

Serviços de arquivos na AWS, como [Amazon EFS](https://aws.amazon.com/efs/) e [Amazon FSx](https://aws.amazon.com/fsx/), oferecem sistemas de arquivos gerenciados que suportam protocolos padrões. O EFS é totalmente gerenciado e fácil de usar, ideal para cargas de trabalho sensíveis ao desempenho e à escala. O FSx fornece soluções de sistema de arquivos totalmente gerenciadas para aplicações específicas, como FSx for Windows File Server e FSx for Lustre.

- **Amazon EFS**: Oferece um sistema de arquivos elástico que pode escalar automaticamente para petabytes de dados, suportando milhares de conexões simultâneas.
- **Amazon FSx**: Fornece sistemas de arquivos totalmente gerenciados que são otimizados para casos de uso específicos, como FSx for Windows File Server para cargas de trabalho Windows nativas e FSx for Lustre para computação de alta performance.

#### Analogia

O armazenamento na AWS pode ser comparado a diferentes tipos de instalações de armazenamento para seus pertences. O Amazon S3 é como um armazém de autoatendimento para guardar objetos que você não precisa acessar com frequência, mas quer manter seguros. O EBS é como um armário de armazenamento seguro para itens valiosos que você usa regularmente. E o EFS/FSx são como unidades de armazenamento especializadas, oferecendo condições ideais para itens específicos que requerem condições particulares de armazenamento.

### Sistemas de Arquivos em Cache: AWS Storage Gateway

O [AWS Storage Gateway](https://aws.amazon.com/storagegateway/) é um serviço híbrido de armazenamento em nuvem que permite às empresas estender e conectar de forma segura seu armazenamento on-premises à nuvem da AWS. Ele fornece três tipos de gateways: File Gateway, Volume Gateway e Tape Gateway, cada um projetado para casos de uso específicos. O serviço facilita o armazenamento de dados na AWS, a redução de custos de armazenamento local e o backup e arquivamento eficientes, integrando-se perfeitamente aos sistemas existentes.

- **File Gateway**: Permite o armazenamento de arquivos baseados em objetos na AWS, acessíveis via protocolos de armazenamento de arquivos padrão da indústria. É ideal para arquivamento de cold data e backup.
- **Volume Gateway**: Fornece armazenamento em bloco para aplicativos usando iSCSI, com dados armazenados em volumes EBS na AWS. Oferece opções de volumes armazenados e em cache, suportando backup eficiente e uso de DR (Disaster Recovery).
- **Tape Gateway**: Oferece uma solução de virtualização de fitas para backup e arquivamento na AWS, compatível com as políticas de backup existentes, facilitando a migração para a nuvem sem alterar os fluxos de trabalho existentes.

O AWS Storage Gateway pode ser visto como um serviço de entrega expressa que facilita a transferência de suas caixas de armazenamento (dados) do seu armazém local (data center on-premises) para um armazém centralizado e seguro (AWS). Dependendo do tipo de caixa ou do conteúdo dentro dela, você escolhe o serviço de entrega (gateway) mais adequado para garantir que tudo chegue ao destino de forma eficiente e segura.

### Políticas de Ciclo de Vida e AWS Backup

#### Políticas de Ciclo de Vida do Amazon S3

As políticas de ciclo de vida do Amazon S3 ajudam a gerenciar seus dados automaticamente, movendo-os para classes de armazenamento mais custo-efetivas ou excluindo-os automaticamente após o término do seu ciclo de vida útil. Essas políticas são cruciais para otimizar os custos de armazenamento e garantir a conformidade com políticas de retenção de dados.

- **Transições**: Automatizam a movimentação de objetos entre classes de armazenamento, por exemplo, de S3 Standard para S3 Standard-IA (Infrequent Access) ou para S3 Glacier para arquivamento de longo prazo.
- **Expirações**: Configuram a exclusão automática de objetos após um período de tempo definido, facilitando o gerenciamento do ciclo de vida dos dados e reduzindo custos desnecessários de armazenamento.

#### AWS Backup

O [AWS Backup](https://aws.amazon.com/backup/) é um serviço centralizado que simplifica o backup de dados e a recuperação em serviços AWS. Ele permite a criação de políticas de backup automáticas, seguras e unificadas, facilitando a conformidade, minimizando riscos e melhorando a eficiência operacional.

- **Centralização**: AWS Backup integra-se com diversos serviços AWS, como EBS, RDS, DynamoDB, e EFS, permitindo gerenciar backups de vários serviços em um único lugar.
- **Recuperação**: Facilita a restauração de dados de backups em caso de perda de dados ou falhas, garantindo a continuidade das operações de negócios e a integridade dos dados.

#### Analogia

Pense no AWS Backup como um plano de seguro abrangente para sua casa (infraestrutura AWS). Assim como um seguro protege contra perdas inesperadas, o AWS Backup assegura que você possa recuperar rapidamente seus dados e aplicações em caso de problemas, mantendo sua "casa" operacional e seus "bens" (dados) seguros.