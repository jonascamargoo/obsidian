---
tipo: conceito
area: Redes
tags:
- redes
criada: '2025-01-23'
---

#### **Áreas Funcionais de Gerenciamento de Redes**

A **OSI** dividiu o gerenciamento de redes em cinco áreas principais:

1. **Gerenciamento de Falhas**  
    Identifica problemas e os resolve rapidamente.
    - Exemplo: Um alerta ao administrador sobre a queda de um link entre escritórios.
    
1. **Gerenciamento de Configuração**  
    Controla e documenta os dispositivos da rede.
    - Exemplo: Atualizar o firmware de um roteador sem precisar ir fisicamente ao local.
    
1. **Gerenciamento de Desempenho**  
    Garante que a rede opere com a melhor eficiência possível.
    - Exemplo: Por que uma conexão de 1 Gbps está funcionando a 100 Mbps?

1. **Gerenciamento de Segurança**  (área à parte)
    Protege os dados e recursos da rede contra acessos não autorizados.
    - Exemplo: Monitorar acessos a pastas restritas às 3h da manhã.

1. **Gerenciamento de Contabilização**  
    Monitora o uso de recursos para controle e planejamento.
    - Exemplo: Saber qual departamento utiliza mais a impressora corporativa.
    - Exemplo: Quem mais utiliza a HTTP as 15h?

### **Protocols for Network Management**

Protocols are essential for monitoring and controlling networks. Key protocols include:

**ICMP (Internet Control Message Protocol)**

Used in tools like `ping`(Mensagem ICMP Echo Request – Resposta: ICMP Echo Reply) and `tracert` (Uso de campo TTL do protocolo IP – Enquanto receber mensagens de descarte sabe que não chegou ao final – Chega ao destino com um Echo Reply) for connection diagnostics. É considerado parte da camada de network, entretando é encapsulado em um pacote IP:

![[Pasted image 20250123082456.png]]

![[Pasted image 20250123082529.png]]

As mensagens podem ser classificadas como requisições ou erros – nenhuma mensagem de erro pode ser gerada em resposta a outra mensagem de erro.
#### **SNMP (Simple Network Management Protocol)** 

A standard protocol for managing network devices such as switches, routers, and servers.

**Real-world Example of SNMP:**  
In a corporate environment, SNMP can alert administrators to high CPU usage on a server, allowing preventive measures to be taken before a system crash occurs.

* Não orientado à conexão - nenhuma ação prévia é necessária no envio de mensagens. Nem pós, portanto, sem garantia;
* Na prática, a maioria das mensagens são entregues e, as não entregues, podem ser retransmitidas;
* Robustez: como não existe conexão, nem o gerente nem o sistema gerenciado necessitam um do outro para operar.
* Cada endereço IP pode possuir vários agentes SNMP, mas de forma geral tem-se apenas um gerente e várias expansões do mesmo
* Agentes SNMP podem ser encontrados em:
	* Hubs mais sofisticados
	* Servidores de rede e seus sistemas operacionais
	* Placas de rede mais sofisticadas e respectivos hosts
	* Dispositivos de rede como switch’s e roteadores
	* Equipamentos de testes como analisadores e monitores de rede
	* No-breaks
	* Modem
	* Servidores Web
	* Servidores de FTP
##### Mensagens SNMP
Versão + header de auth + PDU (protocol data units). Há 5 tipos de PDUs: GetRequest, GetNextRequest, GetResponse, SetResponse e Trap:

![[Pasted image 20250123084443.png]]

![[Pasted image 20250123084630.png]]

## Arquitetura de Gerenciamento Baseada na Web
### O que é?

Uma interface de gerenciamento baseada em navegador é uma ferramenta que permite a administração e o controle de sistemas, aplicativos ou plataformas digitais diretamente através de um navegador web. Em vez de utilizar softwares específicos instalados localmente, o usuário acessa uma interface web para realizar todas as suas tarefas de gerenciamento.

**Como funciona?**

1. **Armazenamento:** As informações e configurações a serem gerenciadas são armazenadas em um servidor web (WebServer). Este servidor armazena todos os dados necessários para que a interface funcione corretamente.
2. **Acesso:** O usuário acessa a interface de gerenciamento através de um navegador web (como Chrome, Firefox, Edge, etc.). Ao digitar o endereço da interface no navegador, ele está, na verdade, solicitando ao servidor web as informações necessárias para exibir a interface.
3. **Exibição:** O servidor web processa a solicitação e envia as páginas HTML, CSS e JavaScript para o navegador. O navegador interpreta esses arquivos e exibe a interface gráfica do usuário (GUI) na tela.
4. **Interação:** O usuário interage com a interface através do navegador, realizando as ações desejadas. Essas ações são enviadas de volta ao servidor web, que as processa e atualiza as informações armazenadas.

**Vantagem: Independência de Plataforma**

- **Acessibilidade:** A principal vantagem é a independência de plataforma. Como a interface é acessada através de um navegador, qualquer dispositivo com um navegador web (computador, smartphone, tablet) pode ser utilizado para gerenciar o sistema, desde que haja uma conexão com a internet.
- **Facilidade de uso:** Não é necessário instalar nenhum software específico, basta abrir o navegador e digitar o endereço.
- **Atualizações:** As atualizações da interface são centralizadas no servidor web, garantindo que todos os usuários sempre tenham acesso à versão mais recente.

![[Pasted image 20250123091934.png]]


## Management Information Base (MIB)

### O que é uma MIB?

Uma MIB (Management Information Base) é, em essência, um **dicionário** que descreve a estrutura e o conteúdo de um dispositivo de rede. Essa estrutura é organizada em forma de árvore, onde cada ramo representa uma parte específica do dispositivo, como interfaces de rede, processos, ou configurações.

**Conceitos-chave:**

- **Base de dados conceitual:** A MIB define como os dados são organizados e relacionados, mas os dados em si podem estar armazenados em diferentes locais, como um banco de dados ou diretamente no dispositivo.
- **Hierarquia:** A MIB é estruturada em uma hierarquia, com nós pai e filho. Os nós pai representam categorias mais gerais, enquanto os nós filho representam informações mais específicas.
- **Objetos:** Os nós que não possuem subnós são chamados de objetos e possuem um valor associado, como a taxa de utilização de um link ou o estado de uma interface.

### Identificando os Elementos da MIB

Cada elemento da MIB possui um identificador único chamado **OID (Object Identifier)**. O OID é uma sequência de números que define a localização do elemento na árvore da MIB.

- **Estrutura do OID:** O OID de um elemento é composto pelo OID de seu pai, seguido do seu próprio identificador.
- **Raiz da MIB:** A raiz da MIB não possui OID.
- **Percurso da Árvore:** A árvore da MIB é percorrida em profundidade, começando pelos ramos da esquerda e seguindo para a direita.

![[Pasted image 20250123093115.png]]
### Arquivo MIB

Um arquivo MIB é um texto que descreve a estrutura e os elementos de uma MIB específica. Ele contém informações como:

- **Nome do objeto:** Um nome descritivo para o objeto.
- **Tipo de dado:** O tipo de dado do objeto (inteiro, string, etc.).
- **Acesso:** Se o objeto pode ser lido, escrito ou ambos.
- **Descrição:** Uma descrição textual do objeto.

**Por que as MIBs são importantes?**

- **Gerenciamento de redes:** As MIBs permitem que ferramentas de gerenciamento de rede (como SNMP) descubram e monitoriem dispositivos de rede de forma padronizada.
- **Automação:** As MIBs podem ser utilizadas para automatizar tarefas de configuração e monitoramento de redes.
- **Interoperabilidade:** As MIBs garantem que diferentes dispositivos de diferentes fabricantes possam ser gerenciados de forma consistente.