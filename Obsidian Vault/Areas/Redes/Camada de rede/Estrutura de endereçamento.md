
## Estrutura de um Endereço IP: Rede e Host

Um endereço IP (IPv4) é um número de 32 bits dividido em quatro octetos (cada octeto possui 8 bits). Esse endereço IP identifica dispositivos individuais em uma rede e também identifica a rede à qual esses dispositivos pertencem.

Essas duas partes – **endereço de rede** e **endereço do host** – têm papéis diferentes:

- **Endereço de Rede**: Define a rede em que o dispositivo (host) está localizado. Todos os dispositivos na mesma rede compartilham o mesmo endereço de rede.
- **Endereço do Host**: Identifica especificamente um dispositivo dentro dessa rede.

Por exemplo, em uma rede doméstica, o endereço `192.168.1.0` pode representar a **rede**, e `192.168.1.5` pode representar um **host específico** nessa rede.

### 2. Máscara de Sub-rede e Separação de Rede e Host

Uma **máscara de sub-rede** é um valor binário que determina quais bits do endereço IP pertencem ao endereço de rede e quais pertencem ao endereço do host. A máscara de sub-rede "separa" o endereço IP em duas partes:

- Os **bits "1"** na máscara indicam os bits que representam a **rede**.
- Os **bits "0"** na máscara indicam os bits que representam o **host**.

Por exemplo:

- **Endereço IP**: `192.168.1.10`
- **Máscara de sub-rede**: `255.255.255.0` (em binário, `11111111.11111111.11111111.00000000`)

Com essa máscara, os três primeiros octetos (`192.168.1`) representam a **rede** e o último octeto (`10`) representa o **host**.

### 3. Exemplo Prático: Divisão de Rede e Host

Vamos ver como isso funciona com um exemplo:

- **Endereço IP**: `192.168.1.10`
- **Máscara de Sub-rede**: `255.255.255.0`

## Classes IPv4

O sistema de classes foi desenvolvido para organizar os endereços IPv4 em categorias, facilitando a alocação de endereços para diferentes tipos e tamanhos de redes. Cada classe de endereço foi projetada para atender diferentes necessidades, dependendo do tamanho da rede e do número de dispositivos conectados.
### Estrutura de Classes IPv4

Originalmente, o IPv4 foi dividido em cinco classes: **Classe A, Classe B, Classe C, Classe D e Classe E**. Cada classe é identificada pelos bits iniciais do endereço e tem uma faixa específica de endereços.

#### Classe A

- **Formato**: `0xxxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx` (primeiro bit é `0`).
- **Faixa**: 1.0.0.0 a 126.255.255.255.
- **Máscara de Sub-rede Padrão**: 255.0.0.0 (/8).
- **Identificação da Rede e Hosts**:
    - Os primeiros 8 bits (ou o primeiro octeto) representam a **identificação da rede**.
    - Os 24 bits restantes representam a **identificação dos hosts**.
- **Quantidade de Redes e Hosts**:
    - Redes: 128 redes (porém apenas 126 são usáveis, pois as faixas 0.x.x.x e 127.x.x.x têm usos especiais).
    - Hosts: Cerca de 16 milhões de hosts por rede.
- **Uso Comum**: Grandes corporações e instituições governamentais. Devido à enorme quantidade de endereços disponíveis por rede, redes Classe A foram atribuídas principalmente a organizações com muitos dispositivos.

#### Classe B

- **Formato**: `10xxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx` (dois primeiros bits são `10`).
- **Faixa**: 128.0.0.0 a 191.255.255.255.
- **Máscara de Sub-rede Padrão**: 255.255.0.0 (/16).
- **Identificação da Rede e Hosts**:
    - Os primeiros 16 bits (ou dois primeiros octetos) representam a **identificação da rede**.
    - Os 16 bits restantes representam a **identificação dos hosts**.
- **Quantidade de Redes e Hosts**:
    - Redes: Cerca de 16.384 redes.
    - Hosts: Cerca de 65.534 hosts por rede.
- **Uso Comum**: Empresas e universidades de médio porte, que precisavam de mais endereços de host, mas não tantos quanto as grandes organizações que usavam Classe A.

#### Classe C

- **Formato**: `110xxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx` (três primeiros bits são `110`).
- **Faixa**: 192.0.0.0 a 223.255.255.255.
- **Máscara de Sub-rede Padrão**: 255.255.255.0 (/24).
- **Identificação da Rede e Hosts**:
    - Os primeiros 24 bits (ou três primeiros octetos) representam a **identificação da rede**.
    - Os 8 bits restantes representam a **identificação dos hosts**.
- **Quantidade de Redes e Hosts**:
    - Redes: Cerca de 2 milhões de redes.
    - Hosts: 254 hosts por rede (considerando que dois endereços são reservados para o endereço de rede e o endereço de broadcast).
- **Uso Comum**: Pequenas redes e redes locais (LANs), sendo amplamente utilizadas em redes domésticas e pequenas empresas.

#### Classe D

- **Formato**: `1110xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx` (quatro primeiros bits são `1110`).
- **Faixa**: 224.0.0.0 a 239.255.255.255.
- **Máscara de Sub-rede Padrão**: Não possui máscara padrão, pois não é destinada a redes de host.
- **Uso**: Reservada para **multicast**, uma tecnologia que permite enviar dados de um único remetente para múltiplos destinatários simultaneamente. Cada endereço de Classe D representa um grupo multicast específico, permitindo que vários dispositivos "assinem" esse grupo para receber pacotes destinados a ele.

#### Classe E

- **Formato**: `11110xxx.xxxxxxxx.xxxxxxxx.xxxxxxxx` (cinco primeiros bits são `11110`).
- **Faixa**: 240.0.0.0 a 255.255.255.255.
- **Máscara de Sub-rede Padrão**: Não possui máscara padrão, pois não é destinada a redes de host.
- **Uso**: Reservada para **pesquisa e desenvolvimento**. Não é usada em redes públicas ou privadas. É um bloco reservado pela IETF (Internet Engineering Task Force) para experimentos e para possíveis futuras expansões, mas não está disponível para uso geral na Internet.

### Porque o Sistema de Classes foi Abandonado

O sistema de classes foi criado quando a Internet ainda era muito menor e mais segmentada, mas, conforme o número de dispositivos cresceu, as classes tornaram-se rígidas e limitadoras. Muitas redes pequenas desperdiçavam endereços, pois a Classe A ou B oferecia mais endereços do que o necessário, mas a Classe C era muito pequena.

Assim, o sistema de **CIDR (Classless Inter-Domain Routing)** foi desenvolvido para oferecer uma maneira mais eficiente e flexível de alocar endereços, permitindo que qualquer tamanho de bloco de endereços fosse atribuído com base nas necessidades reais, sem as limitações de Classes A, B e C.

## Explicando o /8, /16 ou /24

Quando dizemos que a máscara de sub-rede é **/8**, significa que os **8 primeiros bits** do endereço IP são usados para identificar a **rede**. Os bits restantes (no caso do IPv4, são 32 - 8 = 24 bits) são usados para identificar os **hosts** dentro dessa rede.

### Máscara de Sub-rede e o /8

Em termos de máscara de sub-rede, **/8** é equivalente a `255.0.0.0`. Isso ocorre porque:

- **255** em decimal é `11111111` em binário (8 bits configurados como "1").
- A máscara `255.0.0.0` significa que os **8 bits** mais à esquerda são usados para a **rede**, enquanto os **24 bits** restantes são para os hosts.

Então, um endereço de Classe A (com máscara padrão /8) usa os 8 primeiros bits para a rede e os 24 bits restantes para os hosts.

### Exemplo de Endereço IPv4 com /8

Vamos tomar um exemplo:

- **Endereço IP**: `10.0.0.1`
- **Máscara de Sub-rede**: `/8` ou `255.0.0.0`

Nesse caso:

1. **Rede**: Os primeiros 8 bits representam a rede, então `10.0.0.0` é o **endereço de rede**.
2. **Hosts**: Os 24 bits restantes (os três últimos octetos `0.0.1`) são usados para identificar hosts na rede `10.0.0.0`.

### Resultados da Máscara /8

Com uma máscara de sub-rede /8:

- Existe um grande número de endereços de host possíveis (cerca de 16 milhões), pois os 24 bits restantes são dedicados a endereçar dispositivos dentro dessa rede.
- A faixa de endereços possível na rede `10.0.0.0/8` vai de `10.0.0.1` até `10.255.255.254` (sendo `10.255.255.255` o endereço de broadcast da rede).

### Resumo

- **/8** significa que os **8 bits iniciais** representam a **rede**.
- A notação `/8` é equivalente à máscara `255.0.0.0`.
- **Aplicação**: Usado em redes de Classe A, onde há uma grande quantidade de endereços de host para cada rede, adequada para redes muito grandes.

Esse tipo de máscara é útil para endereços Classe A, mas em redes modernas, onde o CIDR é amplamente utilizado, o uso de máscaras flexíveis permite alocar endereços de forma mais eficiente.