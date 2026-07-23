---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-14'
---

## Qual a função?

Sua função é transportar dados na forma de sinais eletromagnéticos por um meio físico de transmissão. Para isso, os dados devem ser transformados em sinais magnéticos. Tanto dados quanto sinais podem ser analógicos ou digitais.

1. **Dados:** São as informações que precisam ser transmitidas. Esses dados podem ser textos, imagens, vídeos, ou qualquer outra forma de informação digital.
    
2. **Sinais eletromagnéticos:** São formas de energia que podem ser transmitidas através do ar, cabos ou fibras ópticas. Esses sinais transportam os dados de um dispositivo para outro na rede. Eles podem ser analógicos ou digitais, dependendo da tecnologia de transmissão e do tipo de dados sendo transmitidos.

## Analógico vs Digital

### Sinais analógicos
São contínuos, podendo representar infinitos valores dentro de um intervalo de tempo. Exemplos são ondas sonoras, sinais de rádio e corrente elétrica, que variam de forma suave e contínua.
### Sinais digitais

São discretos, representados por dois estados distintos, 0 e 1, refletindo a ausência de sinal. Exemplo: linguagem binária usada em computadores. Exemplo: onde os dados são representados por sequências de zeros e uns, e sinais de modulação de amplitude (ASK), modulação de frequência (FSK) e modulação de fase (PSK) usados em comunicação digital.

#### Níveis
Referem-se aos diferentes valores que um sinal pode assumir.
Número de bits por nível é log2 L, onde L é a quantidade de níveis. Exemplos: - 8 níveis = log2 8 = 3 bits, ou seja, cada sinal é representado por 3 bits. - 8 bits = 2^8 = 256 níveis

	![[Pasted image 20240323110911.png]]


### Sinais compostos

Sinais compostos referem-se a sinais que são formados pela combinação de múltiplos componentes individuais, cada um dos quais pode ter diferentes características. Existem dois tipos principais de sinais compostos: periódicos e não periódicos.

#### Sinais periódicos

Completa um padrão dentro de um período mensurável e repete este padrão de forma idêntica nos períodos seguintes: T, 2T, 4T...

	![[Pasted image 20240322213621.png]]

#### Sinais não periódicos

Muda sem exibir um padrão ou ciclo que se repete ao longo do tempo


	![[Pasted image 20240322213744.png]]


## Frequência

Podemos encarar frequência nesse contexto como a taxa de mudança em relação ao tempo:
- Mudanças em curto espaço de tempo = alta frequência;
- Mudanças em longo espaço de tempo = baixa frequência;
- Nível de voltagem constante por todo o tempo = 0 Hz.

### Domínio da frequência

É uma visão gráfica onde usa-se a frequência e não o tempo no eixo horizontal. Facilita a visualização da frequência e da amplitude

	![[Pasted image 20240322215718.png]]


## Bandas de frequência

### Largura de banda (bandwidth)

Corresponde à diferença entre a maior e a menor frequência disponível para a transmissão. Somos bombardeados por várias faixas de frequência regulamentadas, basta sintonizar na frequência correta. A Anatel determina as frequências, exceto as bandas não regulamentadas. Fazendo uma analogia, seria a largura de um cano (quanto maior, maior a vazão) - quantidade de bits que podem passar pelo "cano" por segundo

	![[Pasted image 20240323110218.png]]

 - Largura de banda em hertz (ex: largura de banda da linha telefônica é 4 Khz). 

- Largura de banda em bits por segundo (ex: largura de banda de uma rede Ethernet de 100 Mbps)
### Taxa de transferência 

A taxa de transferência, também conhecida como taxa de dados ou taxa de bits, é uma medida que descreve a quantidade de dados que podem ser transmitidos em uma unidade de tempo, geralmente expressa em bits por segundo (bps). Essa medida é essencial para avaliar o desempenho e a eficiência dos sistemas de comunicação de dados, além de ser a principal, pois frequência por si só não determina. Por que? Como a maioria dos sinais digitais é não periódica, características como frequência e período não são adequadas para descrever esses sinais. Em vez disso, a taxa de transferência é usada como uma medida mais precisa para descrever a capacidade de transmissão de um sinal digital. Ela influencia diretamente o tempo necessário para transmitir arquivos, a qualidade da transmissão em tempo real (como chamadas de vídeo ou streaming de mídia) e outros aspectos do desempenho da rede.
#### Throughput

Há uma diferença entre taxa de transferência e throughput. Taxa de transferência é a medida da **velocidade** na qual os dados são **transmitidos** entre dois pontos - unidades é bps. É influenciada pela largura da banda, tipo de tecnologia de rede, congestionamento da rede, interferências.

Já em relação ao Throughput, pode ser definido como a medida da **quantidade de dados** **transmitidos com sucesso** em um determinado período de tempo, sendo uma medida mais eficiente de desempenho, também em bps. É influenciado por taxa de transferência, tempo de resposta da rede, perdas de dados, erros de transmissão.

Em resumo a  taxa de transferência é a velocidade na qual os dados são transmitidos, em analogia, velocidade máxima de uma via expressa. Por outro lado, throughput é a quantidade de dados transmitidos com sucesso em um determinado período de tempo. Mantendo a analogia, seria o número de carros que passam pela via expressa em um determinado período de tempo.

O Throughput **nunca pode ser superior à Taxa de Transferência**. O Throughput **pode ser menor que a Taxa de Transferência** devido a diversos fatores.
##### Exemplo

Uma conexão de internet com taxa de transferência de 100 Mbps pode ter um throughput de 80 Mbps devido a congestionamento na rede.
#### Limite da taxa de dados

Sabemos que a taxa de dados depende de: largura da banda disponível; nível dos sinais usados; qualidade do sinal (nível de [[Perda na transmissão|ruído]])

##### Sem Com ruídos

Na prática é impossível ter um canal sem ruídos

	$N = 2 \times \text{largura de banda} \times \log_2 L$, Onde L é o número de níveis do sinal. Aumentar o número de níveis do sinal reduz a confiabilidade do sistema (carga excessiva sobre o receptor). O resultado é em bits por segundo.

1 - Considere um canal sem ruído com largura de banda de 3000 Hz transmitindo um sinal com 2 níveis de sinal:

$N = 2 \times 3000 \times \log_2 2 = 6.000 \text{ bps}$ 

##### Com ruídos

1 - Considere um canal com muitos ruídos cujo a relação sinal/ruído é quase zero

$N = B \log_2 (1 + \text{SNR}) = B \log_2 (1 + 0) = B \log_2 1 = B \times 0 = 0$

2 - Taxa de transferência de uma linha telefônica com largura de banda de 3000 Hz (300 a 3300 Hz). A relação sinal/ruído é de 3162

$N = 3000 \log_2 (1 + 3162) = 3000 \log_2 3163 = 3000 \times 11.62 = 34,860 \text{ bps}$

OBS: essa é a capacidade máxima do canal, independente do número de níveis. Não é apenas para  2 níveis para uma taxa de transferência 6 Kbps. Essa fórmula apresentada agora determina que, independente do número de níveis, a capacidade máxima do canal é de 34,86 Kbps

#### Exemplos

1 - Qual a taxa de transferência para baixar documentos textos em 100 páginas por segundo?
	Página de texto = 24 linhas com 80 caracteres por linha
	1 caracter = 8 bits 
	100 x 24 x 80 x 8 = 1.636.000 bps = 1,636 Mbps
	
2 - Taxa de transferência para transmissão em HDTV
	HDTV = 1.920 X 1.080 pixels por tela
	Renovação de tela = 30 vezes por segundo (30 Hz)
	Quantidade de cores = 24 bits (16.777.216 de cores)
	1920 x 1080 x 30 x 24=1.492.992.000 bps=1,5 Gbps
	Obs: são usadas técnicas de compactação que permitem que esta taxa seja em torno de 40 Mbps.

### Throughput vs bandwidth

 A largura de banda define o limite superior teórico da taxa de transferência de um sistema de comunicação.
 No entanto, a taxa de transferência real pode ser influenciada por vários fatores, como a carga de rede, a qualidade do meio de transmissão, a latência e outros. Em condições ideais e sem limitações externas, a taxa de transferência geralmente se aproxima da largura de banda disponível.

- É a medida real pela qual podemos enviar dados pela rede. É inferior à largura de banda
	Uma rede com largura de banda de 10 Mbps permite uma média de 12000 pacotes de 10000 bits por minuto
		Throughput = (10000 x 12000)/60 = 2 Mbps
### Latência

Latência, em termos gerais, é o tempo que um sistema leva para responder a uma solicitação após receber a entrada ou o estímulo. Em contextos de computação e redes, a latência refere-se ao atraso experimentado entre o início de uma operação e sua conclusão. Esse atraso pode ser causado por vários fatores, incluindo processamento, transmissão de dados, espera por recursos e outros.

Quando vários dispositivos fazem requisições através da mesma largura de banda, a largura continua a mesma, portanto os pacotes são enfileirados. Isso causa um aumento na latência. Podemos definir como a soma de 4 componentes:

1. **Tempo de Propagação:**
    - O tempo que leva para os sinais viajarem pelo meio de comunicação, como cabos de cobre, fibras ópticas ou ondas de rádio;
    - Depende da velocidade de propagação do meio, que é geralmente próxima à velocidade da luz no vácuo, mas pode ser mais lenta em meios como cabos de cobre.
2. **Tempo de Transmissão:**
    - O tempo que leva para transmitir todos os bits da mensagem pelo meio de comunicação.
    - Depende do tamanho da mensagem (quantidade de bits) e da largura de banda disponível no meio de comunicação.
3. **Tempo de Fila:**
    - O tempo que a mensagem passa esperando em filas nos dispositivos intermediários da rede, como roteadores e switches.
    - Dependendo do tráfego de rede e da carga dos dispositivos, a mensagem pode enfrentar atrasos adicionais enquanto aguarda para ser encaminhada para o próximo destino.
4. **Retardo de Processamento:**
    - O tempo que é necessário para processar a mensagem nos dispositivos intermediários da rede, como roteadores, switches e firewalls.
    - Isso inclui o tempo para examinar os cabeçalhos dos pacotes, tomar decisões de encaminhamento e realizar outras operações de processamento necessárias.
### 5 GHz e 2,4 GHz

As duas bandas de frequências utilizadas em nossas casas é a 5 GHz e 2,4 GHz. A primeira com maior frequência, ou seja, mais sinais 0 (crista) e 1 (vale) enviados por segundo, porém menor alcance (comprimento):


![[Pasted image 20240309215059.png]]


### Transmissão digital 

Podemos compreender um sinal digital como um sinal analógico composto, com frequências entre 0 (zero) e infinito. O sinal pode ser enviado por transmissão  banda base ou transmissão banda larga. A banda base consiste em enviar o sinal digital por um meio físico sem mudá-lo A transmissão banda-base requer que tenhamos um canal com largura de banda que começa em 0 (zero), conhecido como canal passa-baixa.

### Banda base

Em telecomunicações, a banda base é a frequência utilizada para transmitir os dados de uma rede sem fio. É como se fosse a estrada pela qual as informações trafegam. Existem duas bandas base principais: a de 2,4 GHz e a de 5 GHz.

A banda base também é chamada de sinal passa-baixo, pois pode incluir frequências próximas de zero. Nesse sentido, uma forma de onda sonora é considerada uma banda base, enquanto os sinais de rádio geralmente classificados nos níveis de megahertz não são considerados banda base.
#### Banda base com largura de banda infinita (Placa mãe)

Aqui estamos lidando com canais de passagem única de dados - dedicados,  seria largura de banda infinita entre emissor e receptor, portanto,  mais simples. É vista na placa mãe, por exemplo.

OBS: Por que a deveria ser largura de banda infinita?  Manter um sinal em um nível demanda frequência zero. Então a banda precisa dar suporte à frequência nula,  pois enquanto está em um degrau, não há frequência. Porém a transição de nível é praticamente instantânea, logo demanda frequência infinita.

OBS: largura de banda infinita entre emissor e receptor  é possível em um FSB (placa-mãe), mas não entre 2 computadores de rede: o meio físico não permite. Além disso, largura com banda ampla é algo quase ideal, um exemplo real são os barramentos da placa mãe, mas eles são bem pequenos, tornando possível.


	![[Pasted image 20240323190017.png]]



#### Banda base com largura de banda ampla (LAN)

Em canais passa-baixa com largura de banda ampla ignora-se as frequências da largura de banda que são muito baixas. Exemplos de meios de transmissão incluem cabo coaxial, par trançado e fibra óptica, usados em redes MAN ou as topologias de LANs, mas não entre dispositivos separados. É muito utilizada quando há um sinal por vez sendo transmitido, não tendo que lidar com versatilidade.

Embora o sinal no destino não seja o mesmo sinal original, os dados podem ser deduzidos do sinal percebido. Acontece nas redes locais: barramento, estrela e anel.

#### Banda base com largura de banda limitada (WAN)

Nesse caso, não temos toda a largura de banda para uma transmissão específica, portanto precisamos de formas para executar serviços de forma paralela utilizando a mesma banda. Como o caminho de dados é mais versátil, pode ser que passe por meios onde não é digitalizado, portanto, utiliza-se o conceito de "aproximação do sinal digital por meio de um sinal analógico". Neste caso a largura de banda é proporcional à taxa de transferência.

Neste caso há a aproximação do sinal digital para o sinal analógico. O nível de aproximação depende da largura de banda disponível, podendo ser: Aproximação grosseira ou Melhor aproximação

##### Aproximação grosseira

Na aproximação grosseira, o sinal analógico é aproximado por um sinal digital de forma simplificada, muitas vezes com uma taxa de amostragem relativamente baixa e uma resolução de quantização limitada

–  Considere uma taxa de transferência N e uma taxa de transferência F. Na pior hipótese considere o número máximo de mudanças de um sinal digital, como por exemplo: 01010101 (PIOR CASO) -> F=N/2 ou N=2F (2 bits por ciclo). Ou seja, para 2 bits por ciclo largura de banda é a metade da taxa de transferência.


	![[Pasted image 20240323201333.png]]


##### Aproximação melhorada

 Na aproximação melhorada, são utilizadas técnicas mais avançadas de amostragem e quantização para representar com maior precisão o sinal analógico. Neste caso é necessário maior largura de banda. A largura de banda é proporcional à melhor aproximação do sinal. Isso pode envolver uma taxa de amostragem mais alta e uma maior resolução de quantização, permitindo capturar com mais detalhes as características do sinal analógico. Como resultado, a representação digital é mais fiel ao sinal analógico original, o que pode resultar em uma qualidade de transmissão melhorada e uma menor perda de informação

- Largura de banda= 3 x (taxa de transferência / 2) -> B = 3N/2

- Largura de banda= 5 x (taxa de transferência / 2) -> B = 5N/2
 
	![[Pasted image 20240323203010.png]]

##### Exemplos (ainda considerando o pior caso - 2 bits por ciclo)

1 - Qual a largura de banda necessária para transferência de 1 Mbps em um canal passa-baixa banda base?

Mínima = 1 Mbps / 2 = 0,5 Mhz = 500 Khz 
Melhor resultado = 3 x 1 Mbps /2 = 1,5 Mhz 
Máximo resultado = 5 x 1 Mbps / 2 = 2,5 Mhz

2 - A largura de banda de um canal é de 100 Khz. Qual a maior taxa de transferência suportada neste canal?

100 Khz = Taxa de transferência / 2 
Taxa de transferência = 100 * 2 = 200 Kbps
#### Questões sobre a aproximação de sinal

##### Por que fazer uma aproximação?
- Ela ocorre pois nem todo meio é digital
##### Corrupção de dados
 - Aproximações não são perfeitas (por isso é aproximação), portanto, dados são corrompidos. Para isso, há em camadas superiores à física que lidam com esse problema utilizando algoritmos de recuperação de dados (CRC, por exemplo).
##### Melhorada x Grosseira
 - A grosseira, por não ser preciosista e não tentar ser fiel ao formato digital, tem uma maior taxa de transferência. A melhorada, por sua vez, consome mais recursos (menor taxa de transferência) mas a interpretação do receptor é melhor.
#### Gráfico

No domínio do tempo, quando se visualiza um sinal, como uma onda, em um gráfico, é possível identificar diferentes componentes que representam sua frequência. Aqui está uma explicação sobre os segmentos de retas verticais e horizontais nesse contexto:

	- Reta vertical: frequência infinita
    - Reta horizontal: frequência 0 (zero – sem mudança de frequência)
    - Se um sinal não mudar, sua frequência é zero. Se mudar instantaneamente, sua frequência será infinita

	![[Pasted image 20240323123510.png]]


## Transmissão banda larga - Modulação

Modulação significa transformar o sinal digital em sinal analógico, o inverso pode ser feito também (demodular). Canal passa-faixa -> necessário converter o sinal digital para analógico antes da transmissão

	![[Pasted image 20240323205544.png]]

Praticamente não é utilizada hoje em dia, mas era utilizado como, por exemplo, internet discada, tanto é que ocupava o mesmo canal da telefonia. No contexto da modulação, FSK, ASK e PSK são diferentes técnicas utilizadas para modular sinais de informação em uma onda portadora. Aqui está uma breve explicação de cada uma:

1. **FSK (Frequency Shift Keying):**
    - FSK é uma técnica de modulação onde a informação é codificada pela mudança da frequência da onda portadora.
    - Em FSK, dois ou mais valores de frequência são usados para representar diferentes símbolos ou estados de dados.
    - Por exemplo, em um esquema de FSK binário, um valor de frequência pode representar um bit "0" enquanto outro valor de frequência representa um bit "1".
    
1. **ASK (Amplitude Shift Keying):
    - ASK é uma técnica de modulação onde a informação é codificada pela mudança da amplitude da onda portadora.
    - Em ASK, dois ou mais níveis de amplitude são usados para representar diferentes símbolos ou estados de dados.
    - Por exemplo, em um esquema de ASK binário, uma amplitude mais baixa pode representar um bit "0" enquanto uma amplitude mais alta representa um bit "1".
    
1. **PSK (Phase Shift Keying):**
    - PSK é uma técnica de modulação onde a informação é codificada pela mudança de fase da onda portadora.
    - Em PSK, diferentes valores de fase são utilizados para representar diferentes símbolos ou estados de dados.
    - Por exemplo, em um esquema de PSK binário, uma mudança de fase de 180 graus pode representar um bit "0" enquanto a fase inicial representa um bit "1"

	![[Pasted image 20240323210643.png]]

### Exemplo

 Envio de dados de um computador por linha telefônica: Linha para sinal de voz com largura de banda limitada (4 Khz). 

Como canal passa-baixa = 8 Kbps 
Como canal passa-faixa = uso do modem (conversor digital x analógico) nas extremidades + técnicas de compactação = 56 kbps.



