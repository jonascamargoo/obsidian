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
