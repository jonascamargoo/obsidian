---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-14'
---

Aqui analiso como os dados percorrem seu caminho. Os caminhos são compartilhados por mais de um nó. Hoje em dia os dispositivos conectáveis são se restringem a computadores, portanto, chamamos de "nó". Cada nó compete para enviar seus dados através de um caminho, gerando um grande trafego  que precisa ser gerenciado - trabalho feito por um roteador. Os dados são divididor em pacotes para evitar gargalos. Seria inviável enviar 1 GB de uma vez, enquanto outros dados de outros nós, ou até mesmo do próprio nó, espera o envio.
## LAN

LAN (Local Area Network) é uma rede de computadores que abrange uma área geograficamente limitada, geralmente dentro de um único edifício, campus ou local físico. Uma LAN permite a interconexão de dispositivos, como computadores, impressoras, servidores e dispositivos de armazenamento, facilitando o compartilhamento de recursos e informações entre eles.

As LANs são geralmente construídas com tecnologias de comunicação com fio, como Ethernet. Elas são frequentemente utilizadas em ambientes empresariais, educacionais e residenciais para fornecer conectividade de rede local, permitindo a comunicação de dados, acesso à internet, compartilhamento de arquivos e impressão.

Uma LAN pode ser configurada e gerenciada localmente por uma empresa, instituição ou usuário individual, oferecendo controle direto sobre a infraestrutura e os dispositivos conectados. Elas são fundamentais para a operação de redes corporativas, ambientes de aprendizado, redes domésticas e outros cenários onde a comunicação e o compartilhamento de recursos são essenciais dentro de um espaço físico limitado

- Local Area Network - alta taxa de transferência de dados, cabeada;
- É quem conecta os dispositivos por cabo dentro de um espaço físico

## WAN

WAN (Wide Area Network) é uma rede de comunicação que abrange uma vasta área geográfica, como um país, continente ou até mesmo globalmente, conectando dispositivos e redes locais em diferentes locais geográficos. Ao contrário de LANs (Local Area Networks) e MANs (Metropolitan Area Networks), que operam em áreas geograficamente mais limitadas, as WANs permitem a interconexão de dispositivos e redes em distâncias consideráveis.

As WANs são geralmente construídas com uma combinação de tecnologias de comunicação, incluindo linhas alugadas, circuitos comutados, fibra óptica, satélites e redes de telecomunicações. Elas são amplamente utilizadas por empresas, organizações e provedores de serviços para fornecer conectividade de rede em escala global, permitindo a comunicação de dados, voz e vídeo entre locais remotos.

As WANs desempenham um papel crucial na infraestrutura de comunicação moderna, facilitando a comunicação em larga escala, o acesso à internet, a transferência de arquivos, o compartilhamento de recursos e o acesso a serviços e aplicativos distribuídos geograficamente. Elas são fundamentais para a operação de empresas globais, instituições financeiras, organizações governamentais e provedores de serviços de telecomunicações, garantindo conectividade confiável e eficiente em uma escala global

- Rede de longo alcance (mundial), várias redes integradas, o todo, a internet;
-  Utiliza a infraestrutura do sistema público de telefonia;
- Cabeada;
- Utiliza roteadores (gerenciadores de rotas): se há vários caminhos de dados (rotas) possíveis em várias informações, os roteadores definem dinamicamente qual rota deve ser utilizada por cada pacote;
- Taxa de transferência máxima: 96 Kbps a 100 Mbps;

	![[Pasted image 20240309202118.png]]

## MAN

MAN (Metropolitan Area Network) é uma rede de comunicação que cobre uma área geográfica maior do que uma LAN (Local Area Network), mas menor do que uma WAN (Wide Area Network). Ela conecta vários locais em uma cidade ou área metropolitana, geralmente cobrindo uma área que se estende por vários quilômetros.

As MANs são frequentemente usadas para conectar instituições como campi universitários, empresas, organizações governamentais e centros de dados distribuídos em uma região urbana. Elas geralmente são construídas com uma combinação de tecnologias de comunicação com fio e sem fio, como fibra óptica, Ethernet e redes sem fio de alta velocidade.

Uma MAN fornece uma infraestrutura de rede confiável e de alta velocidade para permitir a comunicação eficiente entre diferentes locais dentro de uma cidade, facilitando o compartilhamento de recursos, acesso à internet, transferência de dados e serviços de telecomunicações. Essa rede é essencial para empresas e organizações que precisam interconectar escritórios e instalações distribuídas em uma área metropolitana para operações comerciais e comunicação eficaz

- Redes metropolitanas (giganet, etc...)
- Públicas, usando os sistemas que antes eram utilizados por TV a cabo: recebe o sinal via satélite e enviar via cabo para as casas

	![[Pasted image 20240309203504.png]]

- Compatível com a LAN
- Cabeada com cabos coaxiais (aqueles de antena com um conector redondo, que chega até a TV) ou fibra óptica
- Cada casa necessita de um cabo de fibra, por isso o emaranhado nos postes
- A MAN também utiliza roteadores, nesse caso aqueles que ficam na residência (os roteadores pertencem à MAN, tanto que eles são fornecidos pelas empresas que prestam o serviço)

	![[Pasted image 20240309210104.png]]


## WLAN

WLAN (Wireless Local Area Network) é uma tecnologia de comunicação sem fio que permite a interconexão de dispositivos dentro de uma área local, como uma casa, escritório, campus universitário ou outro espaço limitado. As WLANs geralmente são baseadas em padrões como IEEE 802.11 (Wi-Fi), que utiliza ondas de rádio para transmitir dados entre dispositivos.

As redes WLAN oferecem conectividade de rede sem a necessidade de cabos físicos, proporcionando flexibilidade na localização e mobilidade dos dispositivos dentro da área coberta pelo sinal sem fio. Dispositivos como computadores, smartphones, tablets, impressoras e outros dispositivos compatíveis com Wi-Fi podem se conectar à rede WLAN para compartilhar recursos, como acesso à internet, impressão e transferência de arquivos.

Comparação:

| Tabela 1: Comparativo entre evolução do Protocolo Ethernet e Wireless LAN |                             |                                |     |
| ------------------------------------------------------------------------- | --------------------------- | ------------------------------ | --- |
| REDE LAN                                                                  | REDE WLAN 802.11            | PUBLICAÇÃO PADRÃO WIRELESS LAN |     |
| Ethernet - 10 Mbps                                                        | 802.11b - 11 Mbps           | 1999                           |     |
| Fast Ethernet - 100 Mbps                                                  | 802.11a/g - 54 Mbps         | 1999 / 2003                    |     |
| Gigabit Ethernet - 1000 Mbps                                              | 802.11n - 75-600 Mbps       | 2009                           |     |
| 10 Gigabit Ethernet - 10 Gbps                                             | 802.11ac - 3,46 Gbps e além | 2012                           |     |


As WLANs são comumente usadas em ambientes domésticos, empresariais e educacionais devido à sua facilidade de implementação, custo relativamente baixo e capacidade de oferecer conectividade de alta velocidade para múltiplos dispositivos simultaneamente. Elas desempenham um papel fundamental na infraestrutura de rede moderna, permitindo a comunicação eficiente e a colaboração entre dispositivos dentro de uma área local.

- Rede local sem fio (wireless)
- Particular
- Access Point: item capaz de gerar uma frequência e quem estiver na área de cobertura e tiver antena (embutida ou não) poderá acessá-la

	![[Pasted image 20240309210753.png]]

- Taxa de transferência: 11, 55, 150, 300, 600 Mbps até 76 Gbps
- A [[Bandas de frequência|largura de banda]] utilizadas é compartilhada entre todos os nós ativos
- Os valores comerciais das taxas de transferências são "falsos", devida à perda (uma LAN ganha de lavada de uma WLAN)
- O access point pode ser simplesmente um access point (repetidor) ou pode assumir o papel de um roteador (mais complexo, requer abstração lógica e configuração)
- Nosso roteador físico utilizado em casa funciona como:
	- Hub: parte que conectamos os outputs do aparelho
	- roteador
	- access point (emissor do wi-fi)

	![[Pasted image 20240309213012.png]]

- Não são regulamentados
- Utilizam a frequência 5 GHz e 2,4 GHz
- Moden é modulador e demodulador, utilizado para converter sinal analógico em digital (como na internet discada). Hoje em dia não é utilizado mais, pois os sinais que chegam já são digitais

## WWAN

WWAN (Wireless Wide Area Network) é uma tecnologia de comunicação sem fio que permite a conectividade de dispositivos em uma área geograficamente ampla, como uma cidade, país ou até mesmo globalmente, através de redes celulares e de satélite. Ao contrário de redes de área pessoal (WPAN) e redes de área local sem fio (WLAN), que têm alcance limitado, as redes WWAN oferecem cobertura em uma escala muito maior.

As tecnologias WWAN mais comuns incluem redes celulares como 3G, 4G LTE e 5G, bem como comunicações via satélite. Essas redes permitem que dispositivos móveis, como smartphones, tablets, laptops e dispositivos de Internet das Coisas (IoT), se conectem à internet e se comuniquem entre si mesmo quando estão fora do alcance de redes locais.

As redes WWAN desempenham um papel crucial na conectividade global, permitindo a comunicação e o acesso à internet em áreas onde as redes locais podem não estar disponíveis ou serem impraticáveis. Elas são essenciais para comunicações móveis, telemetria, rastreamento de frota, monitoramento remoto e muitas outras aplicações em que a conectividade é necessária em áreas vastas ou em movimento

- Rede dos sistemas de telefonia
- Equivalente a WMAN, rede metropolitana sem fio
- Rede de longo alcance sem fio
- Transmissão de dados utilizando o sistema público de telefonia celular
- CCC: central de comunicação e controle - é um conjunto de equipamentos, mais precisamente uma central telefônica que faz o controle das **Estações Rádio Base** (ERB) e permite a comunicação entre outras CCCs, processamento de chamadas, interface com a rede fixa de telefonia e várias outras funções

### ERB (Estação Radio Base)
ERB são as torres de celular. Exercem o papel de controlar os canais e não deixar outras pessoas não ouvirem sua ligação. Estações rádio base fornecem cobertura de sinal para dispositivos móveis dentro de uma determinada área geográfica, chamada de célula. As ERBs se comunicam com os dispositivos móveis usando protocolos celulares específicos, como GSM, CDMA ou LTE. Elas enviam e recebem sinais de rádio dos dispositivos móveis, expandindo a cobertura da rede celular

### CCC (Central de Comunicação e Controle)
São responsáveis por gerenciar o tráfego entre várias ERBs. Uma única CCC pode controlar várias ERBs dentro de uma determinada área geográfica. É responsável por: 

- atribuição de canais de rádio para dispositivos móveis.
- Gerenciamento de handoff (transferência de um dispositivo móvel de uma ERB para outra durante uma chamada).
- Roteamento de chamadas e dados entre ERBs e o núcleo da rede (rede central).


	![[Pasted image 20240309220227.png]]


	Ainda sobre a CCC, ela funciona conectando as EBRs via cabo. Além disso, também são conectadas a dois bancos de dados, um para usuários locais e outros para usuários visitantes. As ligações tradicionais vão para o Sistema Público de Telefonia, enquanto as ligações utilizando internet vão para o router e, por sua vez, para a WAN
	
	![[Pasted image 20240309221604.png]]

### Componentes adicionais

- **Núcleo da Rede:** É a parte central da rede celular, responsável por roteamento de chamadas, autenticação de usuários, gerenciamento de faturamento e interconexão com outras redes (como PSTN e internet).
- **Dispositivos móveis:** Telefones celulares, smartphones, tablets e outros dispositivos equipados com modems celulares que permitem a conexão à WWAN.

### Como funcionam ERBs e CCCs juntos

1. Um dispositivo móvel se conecta à ERB mais próxima com um sinal forte o suficiente.
2. A ERB se comunica com a CCC para estabelecer a conexão.
3. A CCC atribui um canal de rádio ao dispositivo móvel e gerencia a comunicação entre o dispositivo e o núcleo da rede.
4. A CCC pode transferir a conexão do dispositivo móvel para outra ERB (handoff) se o dispositivo se mover para fora da área de cobertura da ERB atual.
#### WPAN

WPAN (Wireless Personal Area Network) é uma rede sem fio de área pessoal que se refere a uma rede de comunicação de curto alcance projetada para interconectar dispositivos eletrônicos pessoais em uma área limitada, como em torno de uma pessoa ou dentro de uma sala. O WPAN utiliza tecnologias sem fio, como Bluetooth, Zigbee e NFC (Near Field Communication), para permitir a comunicação e o compartilhamento de dados entre dispositivos próximos de maneira eficiente e conveniente. Essas redes são comumente usadas para conectar dispositivos como smartphones, tablets, laptops, fones de ouvido sem fio, smartwatches e dispositivos domésticos inteligentes, possibilitando a troca de informações, controle remoto e automação de dispositivos em um ambiente pessoal ou residencial

- Rede pessoal sem fio, possui baixo consumo de energia e baixa taxa de transferência (2 a 10 Mbps)
- Pequeno alcance (área de cobertura). Tipicamente 10 metros
- Exemplos são Bluetooth, RFid e RSSF

## Lista de exercícios

### 1 - “Em termos de desempenho e segurança uma WLAN não substitui uma LAN”. Justifique esta afirmativa.

A superioridade no desempenho das LANs em comparação com as WLANs é influenciada por diversos fatores, tais como o meio de transmissão e a largura de banda. Nas redes LANs, os dados são transmitidos através de cabos de cobre ou fibras ópticas, que são menos suscetíveis a interferências e perdas de sinal do que as ondas de rádio utilizadas em redes sem fio.

No entanto, a eficiência de cada tipo de rede depende das necessidades específicas do usuário. Embora as LANs possam oferecer inicialmente um desempenho superior, elas podem não ser adequadas para dispositivos móveis, o que limita sua utilidade em certos cenários. Por outro lado, em termos de segurança, as conexões cabeadas são imbatíveis, pois o acesso à rede é restrito aos indivíduos que possuem acesso físico ao cabo de rede.

Portanto, a escolha entre LAN e WLAN depende de uma série de fatores, incluindo requisitos de desempenho, mobilidade e segurança, e deve ser feita com base nas necessidades específicas de cada ambiente e usuário.


### 2 - A figura abaixo ilustra uma solução de automação WPAN. Qual é esta solução WPAN empregada? Explique o uso desta tecnologia neste cenário.

		![[Pasted image 20240324100103.png]]

A solução WPAN empregada é a RFID (Radio-Frequency Identification), que é baseada na identificação de objetos por meio de radiofrequência. Inicialmente, os livros recebem etiquetas contendo um chip e sua antena correspondente. Com essas etiquetas, os livros são eletronicamente identificados e podem ser lidos por um leitor RFID.

Quando um cliente deseja retirar um livro, ele pode fazer isso através do atendimento ao cliente ou utilizando um serviço de busca automatizado. Durante o check-out, o atendente lê a etiqueta do livro com o leitor RFID, registrando assim a retirada do livro no sistema. Alternativamente, o cliente pode realizar o check-out de forma autônoma, utilizando um leitor RFID disponível na biblioteca.

Após o check-out, o cliente passa por um detector anti-furto, que realiza outra leitura por radiofrequência para verificar se o check-out foi de fato concluído. Esse processo é importante para garantir a segurança dos materiais da biblioteca.

Quando um livro é devolvido, ele passa por um processo de check-in utilizando a mesma tecnologia RFID. Isso permite que o livro retorne ao acervo da biblioteca e fique disponível para o próximo usuário.

### 3 - Analise

Esta é a planta baixa da futura Escola da Fundação XPTO. O objetivo é apresentar um projeto de hardware para a rede de computadores do prédio. As áreas de trabalho (AT), painéis de telecomunicações (PT) e sala de equipamentos (SE) já estão definidos e identificados na planta. Todos os computadores adquiridos, inclusive os servidores, estão equipados com adaptadores de rede (placa de rede) de 100/1000 Mbps. Além das ATs identificadas acima, há mais 2 servidores que ficam no Núcleo de Manutenção e devem estar conectados à LAN. No Núcleo de Manutenção fica a Sala de Equipamentos e, além de ser a chegada do link de WAN ADSL 5 Mbps para conexão à Internet, ficam também os centralizadores (hubs e/ou switchs) do backbone. A rede deverá trabalhar a 1 Gbps. Os setores de Informática e de Compras da Fundação XPTO fizeram uma pesquisa de componentes de rede, com foco em qualidade e custo, e disponibilizaram a lista a seguir. Nem todos os componentes serão usados no projeto e outros componentes podem ser usados, caso sejam necessários. 

		![[Pasted image 20240324190447.png]]

##### Patch Panels

Patch Panel consiste em uma estrutura metálica que contém uma série de conectores (geralmente RJ45 para cabos de rede Ethernet) dispostos em linhas ou blocos. Cada conector é conectado a um cabo de rede que vem de uma área específica da rede, como uma Área de Trabalho (AT), outro patch panel, ou até mesmo um dispositivo de rede, como um switch. Fica dentro dos Racks, sendo responsável por organizar e direcionar os cabos UTP que chegam nele.
#### a) A melhor solução para o cenário apresentado é uma LAN, WAN, MAN ou uma combinação de ambas. Justifique sua resposta. 



A resposta é "uma combinação de ambas". Temos claramente uma infraestrutura que atende as necessidades de cabeamento. Se o local possui PT, então significa que a conexão cabeada entre a SE e as AT são plenamente possíveis. Com isso, a rede ideal para conectar as AT seriam uma LAN, por desempenho e segurança. Nesse sentido, resolvemos a questão da Ethernet. Pensando em uma conexão com a internet, precisa-se de uma combinação com as outras redes. Em função dessa questão, é indispensável a presença de uma MAN / WAN para acesso à internet parece ser a melhor solução para o cenário apresentado na Escola da Fundação XPTO. Outro indicativo é a presença de Switch / Hub, que indicam o intuito de comunicação externa. 

#### b) Uma WPAN atenderia alguma situação apresentada no cenário? Justifique sua resposta. 

Não, pois nem entre dispositivos próximos a taxa de transferência suportada por esse tipo de rede atenderia. Precisamos de 100/1000 Mbps, enquanto uma WPAN forneceria 10 Mbps.
#### c) Todo o cenário poderia ser atendido por uma WLAN? Justifique sua resposta.

Sim, considerando que parte dos equipamentos possa não ser utilizados, e que a rede irá operar em 1 Gbps, uma rede WLAN seria extremamente eficiente, considerando a natureza do negócio (uma escola).



