
## Diferença entre modelo de referência e protocolo

### Modelo de referência
Possui estrutura abrangente de camadas e funções. Pode ser teórico, como o OSI, ou prático, como o TCP/IP. Além disso, serve como base para o desenvolvimento de protocolos e tecnologias de rede. É a receita de bolo.
### Protocolo
Possui conjunto de regras as quais definem como os dados são formatados, transmitidos e recebidos entre dispositivos em uma rede. Há uma implementação prática que especifica as ações que cada camada deve tomar para garantir a comunicação. Exemplos são: HTTP, FTP, SMTP, TCP, UDP. É o passo a passo para fazer o bolo.

##   O Modelo OSI e o TCP/IP: Teoria versus Prática

O Modelo OSI e o TCP/IP são dois modelos de referência que definem como a comunicação em redes de computadores funciona. No entanto, eles se diferenciam em sua natureza e aplicação.

O **Modelo OSI**, criado pela ISO em 1984, é um modelo teórico que serve como base para o entendimento da comunicação em redes. Sua estrutura abrangente com 7 camadas define todas as funcionalidades possíveis em redes, desde o nível físico até o nível de aplicação. Apesar de sua importância para o conhecimento teórico, o OSI não é totalmente implementado na prática.

Em contraste, o **TCP/IP** é um modelo de fato que surgiu na década de 1970 e é utilizado na maioria das redes de computadores, como a internet. Sua estrutura mais simples com 4 camadas foca nas funcionalidades essenciais para a comunicação, tornando-o mais prático e fácil de implementar.

**Analogia:**

Imagine a construção de um prédio. O Modelo OSI seria como a planta baixa ideal, com todos os detalhes e funcionalidades possíveis. Já o TCP/IP seria como a planta baixa real, que considera as necessidades práticas e viabilidade da construção.


### OSI

O [modelo OSI](https://pt.wikipedia.org/wiki/Modelo_OSI) é um **modelo de rede de computadores** e significa **open system connection**. É um modelo conceitual com o objetivo de padronizar a comunicação numa rede. É bom lembrar que esse modelo não é implementado comercialmente, sendo uma abstração teórica. Ele é dividido nas seguintes camadas:

 1 - Camada Física
	Nessa camada temos especificações sobre transmissão de dados a nível elétrico, físico, de transmissão de bits sem estruturação. É aqui que falamos de cabos de cobre, fibra óptica, de adaptadores, etc

2 - Camada de Enlace de dados
	Aqui temos uma camada que verifica erros da camada anterior, podendo corrigi-los, e que controla o fluxo de transmissão de dados

3 - Camada de Rede
	Essa camada verifica quem enviou os dados e quem deve recebê-los. Aqui já podemos falar de IP (**[internet protocol](https://pt.wikipedia.org/wiki/Endere%C3%A7o_IP)**), podendo analisar origem, destino e definir qual o caminho dos dados

4 - Camada de transporte
	Como o próprio nome já indica, essa camada se refere ao gerenciamento do transporte dos dados, provenientes da camada de rede. Aqui podemos citar o TCP (**[transmission control protocol](https://pt.wikipedia.org/wiki/Transmission_Control_Protocol)**)

5 - Camada de sessão
	É nessa camada que estabelecemos comunicação entre computadores, com aplicações diferentes, que passam a ficar sincronizados

6 - Camada de apresentação
	Aqui os dados da camada anterior são “traduzidos”, convertidos para um formato em que possam ser usados e transportados para a camada seguinte

7 - Camada de aplicação
	Finalmente, é na camada de aplicação que os dados são utilizados em aplicações que nós conseguimos utilizar. Aqui você já pode pensar no protocolo HTTP(**[hypertext transfer protocol](https://pt.wikipedia.org/wiki/Hypertext_Transfer_Protocol)**), por exemplo.

### TCP/IP

Trata-se de um conjunto de protocolos de comunicação entre computadores desenvolvimento da ARPANET, e o nome vem de dois protocolos que já falamos aqui. Esse foi o modelo implementado pela indústria, tanto nas intranets quanto na internet. Esse conjunto de protocolos, inicialmente dividido em 4 camadas (por vezes é dividido em 5 camadas):

1 - Camada física
	É nessa camada que lidamos com comunicação a nível de hardware, sendo ela responsável por endereçar e traduzir os endereços lógicos e fazer o gerenciamento de tráfego e velocidade. Nem sempre é considerada e, as vezes, é contida pela camada de rede

2 - Camada de transporte
	Aqui os dados são anexados ao IP do computador que os enviou e do destinatário.
		Na suíte de protocolos para a internet, o IP executa a tarefa básica de levar pacotes de dados da origem para o destino. O protocolo IP pode transmitir dados para diferentes protocolos de níveis mais altos, esses protocolos são identificados por um único número de protocolo IP

3 - Camada de transporte
	Essa camada pode resolver problemas de confiabilidade e integridade dos dados e também determinam para qual aplicação eles irão

4 - Camada de aplicação
	Enfim, na camada de aplicação podemos interagir com os dados que chegaram, através de aplicações


	![[Pasted image 20240309190749.png]]




