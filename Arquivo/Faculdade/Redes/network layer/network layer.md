---
tipo: conceito
area: Redes
tags:
- redes
criada: '2025-01-23'
---

A camada de rede é uma das mais importantes nos modelos de comunicação em redes de computadores, como o modelo OSI (Open Systems Interconnection) e o modelo TCP/IP. Ela é responsável por endereçar, rotear e entregar pacotes de dados entre dispositivos, mesmo que estejam em redes diferentes.

---

#### O que é a Camada de Rede?

A camada de rede é responsável por:

- Garantir que os pacotes de dados sejam entregues corretamente entre a origem e o destino.
- Realizar o roteamento entre redes, mesmo que os dispositivos estejam em localizações distintas.
- Fornecer um sistema de endereçamento lógico para identificar os dispositivos na rede.

No modelo OSI, a camada de rede é a terceira camada. No modelo TCP/IP, ela é equivalente à camada Internet.

---

#### Funções Principais da Camada de Rede

1. **Endereçamento Lógico**
    
    - Cada dispositivo recebe um endereço lógico (como o endereço IP) para identificação única.
    - Esse endereço é independente do endereço físico (como o endereço MAC da camada de enlace).
2. **Roteamento**
    
    - A camada de rede define o melhor caminho para os dados viajarem entre a origem e o destino.
    - O roteamento é realizado por dispositivos como roteadores.
3. **Fragmentação e Reassemblagem**
    
    - Quando um pacote é muito grande para ser transmitido por um link, ele é dividido em partes menores (fragmentação).
    - No destino, os fragmentos são reagrupados (reassemblagem) para reconstruir o pacote original.
4. **Encapsulamento e Desencapsulamento**
    
    - A camada de rede recebe os dados da camada de transporte, adiciona cabeçalhos (incluindo informações como o endereço IP de origem e destino) e os envia para a camada de enlace.
5. **Controle de Congestionamento**
    
    - Alguns protocolos ajudam a gerenciar o tráfego em redes congestionadas para manter a eficiência.
6. **Qualidade de Serviço (QoS)**
    
    - Define prioridades para diferentes tipos de dados, como voz ou vídeo, garantindo melhor desempenho para tráfegos importantes.

---

#### Protocolos da Camada de Rede

Os principais protocolos usados nesta camada incluem:

- **IP (Internet Protocol):**
    
    - IPv4: Usa endereços de 32 bits e é amplamente utilizado.
    - IPv6: Usa endereços de 128 bits, resolvendo a limitação de endereços do IPv4.
- **ICMP (Internet Control Message Protocol):**
    
    - Utilizado para mensagens de erro e controle na rede (exemplo: comando `ping`).
- **ARP (Address Resolution Protocol):**
    
    - Tradução de endereços IP em endereços físicos (endereços MAC).
- **Protocolos de Roteamento:**
    
    - RIP, OSPF, BGP: Determinam os melhores caminhos para os pacotes.

---

#### Exemplo Prático

Quando você acessa um site na internet:

1. O navegador envia uma solicitação ao endereço IP do site.
2. A camada de rede encaminha a solicitação através da rede local para o roteador.
3. O roteador envia o pacote pela internet, passando por vários roteadores intermediários até alcançar o servidor correto.
4. O servidor responde e o processo ocorre no sentido inverso.

---

#### Resumo

- **Entrada:** Recebe os dados da camada de transporte (protocolo TCP ou UDP).
- **Saída:** Envia pacotes para a camada de enlace para transmissão física.
- **Unidade de Dados:** Pacotes.
- **Dispositivos Associados:** Roteadores.
- **Protocolos Principais:** IPv4, IPv6, ICMP, ARP, entre outros.