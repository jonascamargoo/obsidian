---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-27'
---

### Camada de Enlace

A **camada de enlace de dados** é responsável pela **transferência de dados entre dispositivos na mesma rede local (LAN)**. Esta camada lida diretamente com a comunicação entre dispositivos físicos conectados a uma rede e organiza os dados em unidades chamadas de **quadros (frames)**. A camada de enlace inclui duas subcamadas: a subcamada LLC (Logical Link Control) e a subcamada MAC (Media Access Control).

#### Funções Principais da Camada de Enlace:

1. **Endereçamento Físico**: Na camada de enlace, a comunicação entre dispositivos usa **endereços MAC** (endereços físicos), que são únicos para cada dispositivo de rede. Esses endereços permitem que dados sejam enviados diretamente para um dispositivo específico dentro da mesma rede local.
    
2. **Encapsulamento de Dados em Quadros (Frames)**: A camada de enlace organiza os dados em quadros que contêm não apenas os dados, mas também informações de controle (como o endereço MAC de origem e destino) e um valor de verificação de integridade (checksum) para garantir a integridade dos dados.
    
3. **Detecção e Correção de Erros**: A camada de enlace verifica a integridade dos dados durante a transmissão, o que ajuda a detectar e corrigir erros nos quadros de dados, evitando que dados corrompidos cheguem à camada superior.
    

#### Dispositivo Associado – Switch:

- O **switch** opera na camada de enlace, utilizando endereços MAC para encaminhar quadros entre dispositivos na mesma rede local. Ele mantém uma **tabela de endereços MAC** para saber qual dispositivo está conectado a cada porta, permitindo o envio direto de dados ao dispositivo correto sem broadcast.
- O switch não lida com endereços IP nem toma decisões de roteamento; ele encaminha quadros com base nos endereços MAC.

### Camada de Rede (Camada 3)

A **camada de rede** é responsável pelo **roteamento de pacotes entre redes diferentes**. Ela organiza os dados em unidades chamadas **pacotes (packets)** e usa **endereços IP** para identificar a origem e o destino dos pacotes em redes distintas. A camada de rede permite que dispositivos em redes diferentes se comuniquem e fornece os meios para direcionar pacotes através de múltiplas redes até seu destino final.

#### Funções Principais da Camada de Rede:

1. **Endereçamento Lógico (IP)**: Na camada de rede, os dispositivos são identificados por **endereços IP** (endereços lógicos), que são usados para determinar o caminho entre redes distintas. O endereço IP inclui informações que permitem que os pacotes sejam entregues em qualquer lugar do mundo, não apenas dentro de uma rede local.
    
2. **Encaminhamento e Roteamento**: A camada de rede toma decisões sobre o caminho que os pacotes devem seguir para alcançar seu destino. Essa camada utiliza **protocolos de roteamento** para calcular e decidir a rota mais eficiente para cada pacote, baseado em tabelas de roteamento mantidas pelos roteadores.
    
3. **Fragmentação e Reassemblagem**: A camada de rede também fragmenta pacotes em pedaços menores, se necessário, para que possam passar por redes com restrições de tamanho de pacote. No destino, esses fragmentos são remontados para recriar o pacote original.

#### Dispositivo Associado – Roteador:

- O **roteador** opera na camada de rede e utiliza endereços IP para encaminhar pacotes entre redes diferentes. Ele mantém uma **tabela de roteamento** com informações sobre o caminho mais adequado para enviar pacotes.
- Ao contrário do switch, que opera localmente em uma rede, o roteador é responsável por conectar redes distintas, como uma rede local (LAN) e a Internet, ou diferentes sub-redes.

### Diferenças-Chave entre Camada de Enlace e Camada de Rede

| Aspecto                   | Camada de Enlace (Camada 2)                           | Camada de Rede (Camada 3)                  |
| ------------------------- | ----------------------------------------------------- | ------------------------------------------ |
| **Unidade de Dados**      | Quadro (Frame)                                        | Pacote (Packet)                            |
| **Endereçamento**         | Endereço MAC (físico)                                 | Endereço IP (lógico)                       |
| **Dispositivo Associado** | Switch (operando localmente na rede)                  | Roteador (conecta redes diferentes)        |
| **Função Principal**      | Transferência de dados dentro de uma rede local (LAN) | Roteamento de dados entre redes diferentes |
| **Protocolos Comuns**     | Ethernet, Wi-Fi (MAC)                                 | IP, ICMP, ARP                              |
| **Uso de Tabela**         | Tabela de endereços MAC                               | Tabela de roteamento IP                    |

## Como o dado passa de uma camada para outra?

A transição entre a camada física (Camada 1) e a camada de enlace (Camada 2) é essencial para a comunicação em redes, pois é onde os sinais físicos (eletricidade, luz ou ondas de rádio) são convertidos em dados digitais estruturados (quadros ou "frames"). Essa transição acontece por meio de dispositivos específicos e processos detalhados que transformam os sinais brutos em informações compreensíveis para o restante do sistema.

### Estrutura da Camada Física (Camada 1)

A camada física é a base de toda a comunicação de rede. Ela lida com a **transmissão dos bits brutos** (0s e 1s) através de diversos meios físicos:

- **Cabos de cobre**: Utilizam sinais elétricos (variações de tensão) para representar os bits.
- **Fibra óptica**: Usa pulsos de luz para transmitir informações.
- **Rádio**: Utiliza ondas de rádio (frequências específicas) para comunicação sem fio.

Na camada física, não há estrutura de dados como quadros ou pacotes. Em vez disso, ela apenas transfere sinais que representam bits de dados.

### Passagem da Camada Física para a Camada de Enlace

Quando os sinais chegam ao dispositivo receptor, eles precisam ser **convertidos** para que possam ser interpretados pela camada de enlace. Esse processo envolve duas etapas principais: **conversão de sinal para bits** e **interpretação dos quadros**.

#### 1. Conversão de Sinal para Bits

- Ao receber o sinal (elétrico, óptico ou de rádio), a **interface de rede** do dispositivo (ou seja, a placa de rede, conhecida como **NIC - Network Interface Card**) converte esses sinais físicos em uma sequência digital de 0s e 1s.
- Cada sinal, dependendo de sua intensidade, frequência, ou tempo, é interpretado como um bit.
- Esse processo ocorre muito rapidamente e é feito por componentes eletrônicos no hardware da NIC.

#### 2. Formação e Interpretação dos Quadros (Frames) na Camada de Enlace

- Após a conversão dos sinais para uma sequência de bits, a camada de enlace organiza esses bits em uma unidade de dados chamada **quadro (frame)**.
- A camada de enlace usa **delimitadores** específicos para identificar o início e o fim de um quadro. Os delimitadores são padrões de bits que indicam onde começa e onde termina um quadro.
- Em protocolos como o Ethernet, um quadro possui uma estrutura específica, incluindo:
    - **Cabeçalho do quadro**: Contém informações como os endereços MAC de origem e destino.
    - **Dados ou payload**: É a carga útil, ou seja, a informação que está sendo transmitida.
    - **Trailer (verificação de erro)**: Inclui um valor de verificação (checksum ou CRC) para garantir que os dados não foram corrompidos durante a transmissão.

### Funções da Camada de Enlace na Interpretação dos Dados

Após o quadro ser montado, a camada de enlace executa as seguintes funções para garantir que ele seja entregue corretamente:

1. **Endereçamento MAC**:
    
    - A camada de enlace verifica o **endereço MAC de destino** no cabeçalho do quadro para decidir se ele é destinado ao próprio dispositivo.
    - Caso o quadro seja destinado ao dispositivo, ele é processado; caso contrário, ele é descartado ou, no caso de um switch, encaminhado para a porta correta.
2. **Verificação de Erros**:
    
    - A camada de enlace usa o **checksum ou CRC (Cyclic Redundancy Check)** para verificar a integridade dos dados no quadro.
    - Se o valor de verificação não corresponder ao esperado, o quadro é descartado, e o dispositivo pode solicitar uma retransmissão, dependendo do protocolo.
3. **Entrega do Quadro para Camadas Superiores**:
    
    - Se o quadro passa na verificação de erros e é destinado ao dispositivo, a camada de enlace remove o cabeçalho e o trailer, deixando apenas os dados.
    - Esses dados são entregues à camada superior, que no modelo OSI é a **camada de rede** (Camada 3), onde os endereços IP e o roteamento são processados.

### Exemplo Prático: Recebimento de um Quadro Ethernet

Suponha que um computador receba um quadro Ethernet através de sua placa de rede:

1. **Recepção de Sinais**: A placa de rede detecta sinais elétricos no cabo Ethernet. Esses sinais representam os bits.
2. **Conversão para Bits**: A placa converte esses sinais em uma sequência de 0s e 1s.
3. **Formação do Quadro**: A camada de enlace organiza essa sequência de bits em um quadro Ethernet, identificando o cabeçalho e o trailer.
4. **Verificação do Endereço MAC**: A camada de enlace verifica se o endereço MAC de destino no quadro corresponde ao da placa de rede.
5. **Verificação de Erros**: O quadro passa por uma verificação de erros usando o valor CRC.
6. **Entrega para a Camada de Rede**: Após a verificação, os dados são entregues para a camada de rede, onde o endereço IP e o roteamento podem ser tratados.

### Resumo

1. **Camada Física**: Transmite sinais físicos brutos que representam bits.
2. **Conversão para Bits**: A NIC converte esses sinais em uma sequência de bits digitais.
3. **Camada de Enlace**: Organiza os bits em quadros, verifica os endereços MAC e a integridade dos dados antes de entregar para as camadas superiores.

### Resumo Final

A camada de enlace conecta dispositivos **dentro da mesma rede local** usando endereços físicos (MAC), enquanto a camada de rede permite a **comunicação entre redes** usando endereços lógicos (IP).

Assim:

- **Switches** operam na camada de enlace, usando endereços MAC para enviar quadros dentro de uma mesma rede local.
- **Roteadores** operam na camada de rede, usando endereços IP para enviar pacotes entre redes diferentes.