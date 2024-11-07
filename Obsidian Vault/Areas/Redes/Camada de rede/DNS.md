## O que é? 

 DNS com uma estrutura de banco de dados hierárquica e distribuída para facilitar uma abordagem mais dinâmica para a resolução de nomes de domínio, capaz de acompanhar o ritmo de uma rede de computadores em rápida expansão. A hierarquia começa com o nível raiz, indicado por um ponto (.) e se ramifica em domínios de nível superior (TLDs) como “.com”, “.org”, “.net” ou TLDs com código de país (ccTLDs). ) como “.uk” e “.jp” e domínios de segundo nível.

## Servidores DNS

### Servidores recursivos

Os **servidores recursivos**, ou **resolvedores de DNS**, são os servidores que realizam o trabalho de buscar a resposta para uma solicitação de DNS em nome do usuário. Esses servidores são configurados para responder às solicitações de resolução de domínio, transformando o nome de domínio (como "example.com") em um endereço IP.

### Funcionamento dos Servidores Recursivos

1. **Recepção de Solicitação do Usuário**  
    Quando um usuário digita um domínio no navegador, a solicitação é enviada ao **servidor recursivo** para iniciar a busca pelo IP associado ao domínio.
    
2. **Busca em Cache**
    - **Cache:** O servidor recursivo armazena em cache respostas DNS temporariamente, definidas pelo valor **TTL** (Time To Live), para tornar as consultas mais rápidas.
    - **Verificação do Cache:** Se o servidor recursivo já tiver a resposta em cache, ele simplesmente retorna a resposta sem necessidade de nova consulta, economizando tempo e recursos.
3. **Consulta ao Sistema DNS (Quando Não Está em Cache)**  
    Se o servidor recursivo não tiver a resposta em cache, ele iniciará uma **série de consultas aos servidores autoritativos** para resolver o domínio.

### Servidores autoritários

- **Topo da Hierarquia: Servidores de Nomes Raiz**
    - **Função:** São responsáveis pela **zona raiz**, ou seja, o ponto central de todo o sistema DNS.
    - **Operação:** Há 13 endereços IP que representam 13 redes de servidores raiz, identificados de **A a M**.
    - **Atuação:** Quando recebem uma consulta, eles **direcionam a solicitação** ao servidor de nomes TLD apropriado (por exemplo, .com, .org, .gov, etc.).
    - **Exemplo:** Se alguém digita “ibm.com”, o servidor raiz indica qual é o servidor TLD responsável pelos domínios .com.

- **Nível Intermediário: Servidores de Nomes TLD (Top-Level Domain)**
    - **Função:** Administram domínios de nível superior (como **.com**, **.gov**, **.org**, etc.).
    - **Operação:** Quando recebem uma solicitação para um domínio, como “ibm.com”, o servidor TLD **encaminha a consulta** para o servidor autoritativo do domínio de segundo nível correspondente (neste caso, ibm.com).
    - **Exemplo:** O servidor TLD de .com lida com todos os domínios que terminam em .com, enquanto o TLD de .gov lida com todos os domínios que terminam em .gov.

- **Nível Inferior: Servidores Autoritativos de Domínios de Segundo Nível**
    - **Função:** São servidores responsáveis pelo armazenamento dos registros DNS definitivos de domínios específicos, como “ibm.com” ou “google.com”.
    - **Operação:** Mantêm os arquivos de zona que vinculam o **nome do domínio completo ao seu endereço IP** correspondente.
    - **Exemplo:** O servidor de nomes autoritativo de “ibm.com” conhece os IPs e outros registros associados ao domínio, e responde diretamente com a informação final para concluir a consulta DNS.


## Como funciona

Toda consulta (também conhecida como solicitação DNS) ao DNS segue a mesma lógica para resolver endereços IP. Quando um usuário insere um URL, seu computador consulta progressivamente os servidores DNS para localizar as informações e os registros de recursos apropriados para atender à solicitação do usuário. Esse processo continua até que o DNS encontre a resposta certa do servidor DNS autoritativo associado a esse domínio.

Mais especificamente, a resolução de consultas ao DNS envolve vários processos e componentes importantes.

#### Início da consulta

Um usuário insere um nome de domínio, como "ibm.com", em um navegador ou aplicativo e a solicitação é enviada para um resolvedor de DNS recursivo. Normalmente, o dispositivo do usuário tem configurações de DNS predefinidas, fornecidas pelo provedor de serviços de internet (ISP), que determinam qual resolvedor recursivo um cliente consulta.

#### Resolvedor recursivo

O resolvedor recursivo verifica seu cache, o armazenamento temporário de um navegador da web ou sistema operacional (como macOS, Windows ou Linux) que contém pesquisas de DNS anteriores, em busca do endereço IP correspondente do domínio. Se o resolvedor recursivo não tiver os dados de pesquisa de DNS em cache, iniciará o processo de busca dos servidores DNS autoritativos, começando pelo servidor raiz. O resolvedor recursivo consulta a hierarquia do DNS até encontrar o endereço IP final.

#### Servidor de nomes raiz

O resolvedor recursivo consulta um servidor de nomes raiz, que responde com uma referência ao servidor de TLD apropriado para o domínio em questão (o servidor de nomes de TLD responsável pelos domínios ".com" neste caso). Ou seja, redireciona para o servidor que contém aquele IP.

#### Servidor de nomes TLD

O resolvedor consulta o servidor de nomes TLD ".com" que responde com o endereço do servidor de nomes autorizado para "ibm.com". Esse servidor também é chamado de servidor de nomes de domínio de segundo nível.

#### Servidor de nomes de domínio (servidor de nomes de domínio de segundo nível)

O resolvedor consulta o servidor de nomes de domínio, que procura o arquivo [de zona DNS](https://www.ibm.com/br-pt/topics/dns-zone) e responde com o registro correto do nome de domínio fornecido.

#### Resolução da consulta

O resolvedor recursivo armazena em cache o registro DNS, por um tempo especificado pelo TTL do registro, e retorna o endereço IP ao dispositivo do usuário. O navegador ou aplicativo pode então iniciar uma conexão com o servidor host nesse endereço IP para acessar o site ou serviço solicitado.

![[Pasted image 20241107152928.png]]

## Arquivos de zona DNS e registros de recursos

  

**Publicado em**19 de abril de 2024  
**Colaboradores:** Chrystal R. China, Michael Goodwin

O que é DNS?

O Sistema de Nomes de Domínio (Domain Name System, DNS) é o componente do protocolo padrão da internet responsável por converter nomes de domínio que podem ser entendidos pelas pessoas nos endereços de protocolo de internet (IP) que os computadores utilizam para identificar uns aos outros na rede.

Muitas vezes chamada de “lista telefônica da internet”, uma analogia mais moderna é que o DNS gerencia nomes de domínio da mesma forma que os smartphones gerenciam contatos. Os smartphones eliminam a necessidade de os usuários memorizarem números de telefone individuais, armazenando-os em listas de contatos pesquisáveis com facilidade.

Da mesma forma, o DNS possibilita que os usuários se conectem a sites com nomes de domínio da internet em vez de endereços IP. Em vez de ter que memorizar que o servidor da web está em "93.184.216.34", por exemplo, os usuários podem simplesmente acessar a página "www.exemplo.com" para receber os resultados desejados.   

GuiaAlcance flexibilidade no local de trabalho com DaaS

Saiba como o desktop como serviço (DaaS) permite as empresas atingirem o mesmo nível de performance e segurança ao implementar aplicações no local.

[](https://www.ibm.com/account/reg/signup?formid=urx-52331)

História do DNS

Antes do DNS, a internet era uma rede crescente de computadores utilizados principalmente por instituições acadêmicas e de pesquisa. Os desenvolvedores associavam manualmente os nomes dos servidores aos endereços IP utilizando um arquivo de texto simples chamado HOSTS.TXT. O SRI International mantinha esses arquivos de texto e os distribuía a todos os computadores na internet. No entanto, com a expansão da rede, essa abordagem tornou-se cada vez mais insustentável. 

Para lidar com as limitações do HOSTS.TXT e criar um sistema mais escalável, Paul Mockapetris, cientista da computação da Universidade do Sul da Califórnia, inventou o sistema de nomes de domínio em 1983. Um grupo de pioneiros da internet ajudou na criação do DNS e foi o autor da primeira solicitação de comentários (RFCs) que detalhava as especificações do novo sistema, RFC 882 e RFC 883. O RFC 1034 e o RFC 1035 substituíram posteriormente os RFCs anteriores.

Eventualmente, com a expansão do DNS, o gerenciamento do DNS tornou-se responsabilidade da internet Assigned Numbers Authority (IANA), antes de finalmente passar para o controle da organização sem fins lucrativos Internet Corporation for Assigned Names and Numbers (ICANN), em 1998.

Conteúdo relacionado

Registre-se para receber o guia sobre nuvem híbrida

[](https://www.ibm.com/account/reg/signup?formid=urx-52611)

Tipos de servidores DNS

Desde o início, os desenvolvedores projetaram o DNS com uma estrutura de banco de dados hierárquica e distribuída para facilitar uma abordagem mais dinâmica para a resolução de nomes de domínio, capaz de acompanhar o ritmo de uma rede de computadores em rápida expansão. A hierarquia começa com o nível raiz, indicado por um ponto (.) e se ramifica em domínios de nível superior (TLDs) como “.com”, “.org”, “.net” ou TLDs com código de país (ccTLDs). ) como “.uk” e “.jp” e domínios de segundo nível.

A arquitetura do DNS consiste em dois tipos de [servidores de DNS](https://www.ibm.com/br-pt/topics/dns-server), servidores recursivos e servidores autoritativos. Os servidores DNS recursivos são os que fazem a "solicitação", procurando as informações que conectam um usuário a um site.

### Servidores recursivos

Os servidores recursivos, também conhecidos como resolvedores recursivos ou resolvedores de DNS, normalmente são gerenciados por provedores de serviços de internet (ISPs), grandes empresas ou outros provedores de serviços de DNS de terceiros. Atuam em nome do usuário final para resolver o nome de domínio de um endereço IP. Os resolvedores recursivos também armazenam em cache as respostas a uma solicitação por um determinado período (definido pelo valor de tempo de vida, ou TTL) para melhorar a eficiência do sistema nas consultas futuras no mesmo domínio.

Quando um usuário digita um endereço da web em um navegador de pesquisa, o navegador conecta um servidor DNS recursivo para resolver a solicitação. Se o servidor recursivo tiver a resposta armazenada em cache, poderá conectar o usuário e concluir a solicitação. Caso contrário, o resolvedor recursivo consultará uma série de servidores DNS autoritativos para encontrar o endereço IP e conectar o usuário ao site desejado.

### Servidores autoritativos

Os servidores autoritativos apresentam as “respostas”. Os servidores de nomes autoritativos mantêm os registros definitivos de um domínio e respondem às solicitações sobre nomes de domínio armazenados em suas respectivas zonas (normalmente com respostas [configuradas pelo proprietário do domínio](https://www.ibm.com/br-pt/blog/how-to-mitigate-the-risks-of-diy-authoritative-dns/)). Há diversos tipos de servidores de nomes autoritativos, cada um servindo uma função específica dentro da hierarquia do DNS.  
  
Os servidores de nomes DNS autoritativos são:

#### Servidores de nomes raiz

Os servidores de nomes raiz ficam no topo da hierarquia do DNS e são responsáveis por gerenciar a zona raiz (o banco de dados central do DNS). Eles respondem a consultas de registros armazenados na zona raiz e encaminham as solicitações ao servidor de nomes do TLD apropriado.

Há 13 endereços IP utilizados para consultar 13 redes de servidores raiz diferentes, identificadas por letras de A a M, que lidam com solicitações para os TLDs e direcionam as consultas para os servidores de nomes de TLD apropriados. A internet Corporation for Assigned Names and Numbers (ICANN) opera essas redes de servidores raiz.

#### Servidores de nomes de domínio de nível superior (TLD)

Os servidores TLD são responsáveis por gerenciar o próximo nível da hierarquia, incluindo domínios genéricos de nível superior (gTLDs). Os servidores de nomes de TLD direcionam as consultas aos servidores de nomes autoritativo para os domínios específicos dentro do seu TLD. Então, o servidor de nomes TLD de ".com" direcionaria domínios que terminam em ".com", o servidor de nomes TLD de ".gov" direcionaria domínios que terminam em ".gov", e assim por diante. 

#### Servidores de nomes de domínio (servidores de nomes de domínio de segundo nível)

O servidor de nomes de domínio (também conhecido como servidor de nomes de domínio de segundo nível) contém o arquivo de zona com o endereço IP do nome de domínio completo, como "ibm.com".

Como funciona o DNS?

Toda consulta (também conhecida como solicitação DNS) ao DNS segue a mesma lógica para resolver endereços IP. Quando um usuário insere um URL, seu computador consulta progressivamente os servidores DNS para localizar as informações e os registros de recursos apropriados para atender à solicitação do usuário. Esse processo continua até que o DNS encontre a resposta certa do servidor DNS autoritativo associado a esse domínio.

Mais especificamente, a resolução de consultas ao DNS envolve vários processos e componentes importantes.

#### Início da consulta

Um usuário insere um nome de domínio, como "ibm.com", em um navegador ou aplicativo e a solicitação é enviada para um resolvedor de DNS recursivo. Normalmente, o dispositivo do usuário tem configurações de DNS predefinidas, fornecidas pelo provedor de serviços de internet (ISP), que determinam qual resolvedor recursivo um cliente consulta.

#### Resolvedor recursivo

O resolvedor recursivo verifica seu cache, o armazenamento temporário de um navegador da web ou sistema operacional (como macOS, Windows ou Linux) que contém pesquisas de DNS anteriores, em busca do endereço IP correspondente do domínio. Se o resolvedor recursivo não tiver os dados de pesquisa de DNS em cache, iniciará o processo de busca dos servidores DNS autoritativos, começando pelo servidor raiz. O resolvedor recursivo consulta a hierarquia do DNS até encontrar o endereço IP final.

#### Servidor de nomes raiz

O resolvedor recursivo consulta um servidor de nomes raiz, que responde com uma referência ao servidor de TLD apropriado para o domínio em questão (o servidor de nomes de TLD responsável pelos domínios ".com" neste caso).

#### Servidor de nomes TLD

O resolvedor consulta o servidor de nomes TLD ".com" que responde com o endereço do servidor de nomes autorizado para "ibm.com". Esse servidor também é chamado de servidor de nomes de domínio de segundo nível.

#### Servidor de nomes de domínio (servidor de nomes de domínio de segundo nível)

O resolvedor consulta o servidor de nomes de domínio, que procura o arquivo [de zona DNS](https://www.ibm.com/br-pt/topics/dns-zone) e responde com o registro correto do nome de domínio fornecido.

#### Resolução da consulta

O resolvedor recursivo armazena em cache o registro DNS, por um tempo especificado pelo TTL do registro, e retorna o endereço IP ao dispositivo do usuário. O navegador ou aplicativo pode então iniciar uma conexão com o servidor host nesse endereço IP para acessar o site ou serviço solicitado.

## Arquivos de zona DNS e registros de recursos

Além dos principais tipos de servidor, o DNS usa arquivos de zona e vários tipos de registro para ajudar no processo de resolução. Arquivos de zona são arquivos baseados em texto que incluem mapeamentos e informações sobre um domínio dentro de uma zona DNS.

Cada linha de um arquivo de zona define um [registro de recursos DNS](https://www.ibm.com/br-pt/topics/dns-records) (uma única parte de informações sobre a natureza de um tipo específico ou parte de dados). Os registros de recursos garantem que, quando um usuário envia uma consulta, o DNS pode converter rapidamente os nomes de domínio em informações acionáveis que direcionam os usuários para o servidor correto. 

Os arquivos de zona DNS começam com dois registros obrigatórios: o tempo de vida global (TTL) — que indica como os registros devem ser armazenados no cache DNS local — e o início da autoridade (registro SOA) — que especifica o servidor de nomes autoritativo primário para a zona DNS.  

Após os dois registros primários, um arquivo de zona pode conter vários outros tipos de registro, incluindo: 

#### Registros A e registros AAAA

Os registros A estão vinculados aos endereços IPv4 e os registros AAAA estão vinculados aos endereços IPv6.

#### Registros de troca de mensagens (registros MX)

Os registros MX definem um servidor de e-mail SMTP de um domínio. 

#### Registros de nomes canônicos (registros CNAME)

[Os registros CNAME](https://www.ibm.com/br-pt/topics/cname) redirecionam nomes de host de um alias para outro domínio (o “domínio canônico”).

#### Registros do servidor de nomes (registros NS)

Os registros NS indicam o servidor de nomes autoritativo de um domínio.

#### Registros de ponteiro (registros PTR)

Os registros PTR definem uma pesquisa DNS reversa, mapeando endereços IP de volta para nomes de domínio.

#### Registros de texto (registros TXT)

Os registros TXT indicam o registro da estrutura da política do remetente para autenticação de e-mail.

## Serviços de DNS público versus privado

#### DNS público

DNS público geralmente refere-se ao lado do resolvedor do DNS e aos servidores recursivos utilizados para consultar servidores de nomes autoritativos e conectar usuários a sites.  

Esses servidores são acessíveis a qualquer usuário na internet e empresas como a Cloudflare (1.1.1.1), O Quad9 e o OpenDNS normalmente oferecem gratuitamente. Os servidores DNS públicos são mantidos pelas organizações que os executam. Usuários e clientes não têm controle sobre operação, políticas ou configuração.         

#### DNS privado

DNS privado geralmente se refere à parte autoritativa do DNS. As organizações configuram servidores DNS privados dentro de uma rede privada e esses servidores atuam como servidores DNS autoritativos, oferecendo pesquisa de DNS para recursos internos. Os servidores DNS privados ficam atrás de um firewall e mantêm somente registros de sites internos, portanto o acesso é restrito a usuários, dispositivos e redes autorizados.

Ao contrário das configurações de DNS público, o DNS privado oferece às organizações o controle sobre seus servidores DNS, permitindo que personalizem registros DNS, apliquem esquemas de nomenclatura internos e apliquem políticas de segurança específicas. Isso significa também que as organizações são responsáveis por manter a [infraestrutura](https://www.ibm.com/br-pt/topics/infrastructure), seja hospedada em [data centers](https://www.ibm.com/br-pt/topics/data-centers) locais ou por meio de [serviços de nuvem](https://www.ibm.com/br-pt/topics/cloud-computing).


## Riscos de segurança

#### Falsificação de DNS

A falsificação de DNS, também chamada de envenenamento de cache, ocorre quando um invasor insere registros de endereços falsos no cache de um resolvedor de DNS, fazendo com que o resolvedor retorne um endereço IP incorreto e redirecione os usuários para sites maliciosos. A falsificação pode comprometer dados confidenciais e levar a ataques de phishing e distribuição de malware.

**Implementação da liberação de DNS:** limpar regularmente o cache do DNS remove todas as entradas do sistema local, o que pode ser útil para excluir registros de DNS inválidos ou comprometidos que possam levar os usuários a sites maliciosos.

**Implementação de extensões de segurança DNS (DNSSECs) e redes virtuais privadas (VPNs):** [o DNSSEC adiciona uma camada de segurança às pesquisas de DNS,](https://www.ibm.com/br-pt/blog/how-is-dnssec-different-from-encryption/) exigindo que as respostas de DNS sejam assinadas digitalmente. Especificamente, o [DNSSEC](https://www.ibm.com/br-pt/topics/dnssec) pode proteger contra ataques de falsificação de DNS autenticando a origem das solicitações e verificando a integridade dos dados DNS.

#### Ataques de ampliação de DNS (DDoS)

A amplificação de DNS é um tipo de ataque [distribuído de negação de serviço](https://www.ibm.com/br-pt/topics/ddos) (DDoS) em que um invasor envia pequenas consultas a um servidor DNS com o endereço de retorno falsificado para o endereço IP da vítima. Esses ataques exploram a natureza sem estado dos protocolos DNS e exploram o fato de que uma pequena consulta pode gerar uma resposta desproporcionalmente grande.

**Emprego de práticas de limitação de taxa:** a limitação de taxa em servidores DNS pode mitigar ataques DDoS restringindo o número de respostas, ou a taxa na qual os servidores enviam respostas, a um único solicitante em um período definido.

**Emprego de redundâncias:** implantar o DNS em uma configuração redundante em vários servidores dispersos geograficamente pode ajudar a garantir a disponibilidade da rede em caso de ataque ou interrupção. Se o [servidor primário](https://www.ibm.com/br-pt/topics/primary-dns) ficar inativo, os servidores secundários poderão assumir os serviços de resolução de DNS.

#### Tunelamento DNS

O encapsulamento DNS é uma técnica utilizada para ignorar medidas de segurança encapsulando tráfego não-DNS, como HTTP, em consultas e respostas DNS. Os invasores podem usar túneis DNS para retransmitir comandos de malware ou para exfiltrar dados de uma rede comprometida, geralmente codificando a carga em consultas e respostas DNS para evitar a detecção.

#### Sequestro de domínio

O sequestro de domínio ocorre quando um invasor obtém acesso não autorizado a uma conta de registrador de domínio e altera os detalhes de registro de um domínio. O sequestro permite que agentes mal-intencionados redirecionem o tráfego para servidores maliciosos, interceptem e-mails e assumam o controle da identidade online do usuário.

**Solicitação de autenticação de dois fatores (2FA) para registradores de domínio:** o estabelecimento de [2FA](https://www.ibm.com/br-pt/topics/2fa) para contas de registrador de domínio pode dificultar o acesso não autorizado nos servidores aos invasores e reduzir o risco de sequestro de domínio.

#### Aquisição de subdomínio

Entradas de DNS negligenciadas para subdomínios que apontam para serviços desativados são os principais alvos dos invasores. Se um serviço (como um host na nuvem) tiver sido desativado, mas a entrada de DNS permanecer, um invasor poderá reivindicar o subdomínio e configurar um site ou serviço malicioso em seu lugar.