---
tipo: conceito
area: Redes
tags:
- redes
criada: '2025-01-10'
---

## O que é?

O FTP (File Transfer Protocol) é um protocolo utilizado para transferir arquivos entre computadores em uma rede, utilizando uma estrutura cliente-servidor. O fluxo descrito envolve várias etapas que garantem a comunicação, autenticação e transferência de dados. Vamos detalhar cada ponto do fluxo de dados mencionado:

## Fluxo do FTP

#### **1. Usuário Inicia o Processo**

O fluxo começa com o **usuário** interagindo com um **agente de usuário FTP**, que normalmente é um software FTP (como FileZilla, WinSCP ou até mesmo o terminal de comandos). O usuário fornece o endereço do servidor FTP (como um domínio ou endereço IP) para que a conexão seja estabelecida.

---

#### **2. Estabelecimento da Conexão**

Após o fornecimento do endereço do servidor, o **cliente FTP local** inicia uma conexão com o **servidor FTP remoto** por meio do protocolo TCP. Esta conexão é estabelecida em duas camadas diferentes, cada uma com uma porta específica:

- **Conexão de Controle:** Porta **TCP 21**. É usada para enviar comandos e receber respostas entre o cliente e o servidor. Por exemplo, comandos para autenticação, navegação de diretórios ou solicitações de transferência de arquivos.
- **Conexão de Dados:** Porta **TCP 20**. É utilizada para a transferência efetiva dos dados, ou seja, os arquivos sendo enviados ou baixados.

A conexão TCP é confiável e orientada à sessão, garantindo que os dados sejam transmitidos corretamente.

---

#### **3. Envio de Credenciais e Comandos**

Após a conexão de controle ser estabelecida, o cliente FTP envia informações de autenticação:

- **ID (nome de usuário):** Identifica o usuário que está tentando acessar o servidor.
- **Senha:** Garante que apenas usuários autorizados tenham acesso.

Além disso, o cliente pode enviar comandos FTP para o servidor, como:

- `LIST`: Listar os arquivos no diretório atual.
- `RETR`: Baixar um arquivo do servidor para o cliente.
- `STOR`: Enviar um arquivo do cliente para o servidor.
- `PWD`: Exibir o diretório atual no servidor.

---

#### **4. Autorização do Servidor**

O servidor verifica as credenciais enviadas pelo cliente. Se a autenticação for bem-sucedida, o servidor autoriza o acesso e monitora o estado da sessão do usuário, como:

- **Conta:** O servidor mantém o controle de qual conta está logada.
- **Diretório Corrente:** O diretório atual no qual o usuário está navegando no servidor.

---

#### **5. Transferência de Arquivos**

Uma vez autenticado e autorizado, o cliente pode solicitar transferências de arquivos. O fluxo ocorre da seguinte forma:

- O cliente envia o comando (como `RETR` ou `STOR`) pela conexão de controle.
- O servidor inicia a **conexão de dados** na porta **TCP 20** para transferir os arquivos solicitados.
- O processo de transferência ocorre e, ao final, o servidor confirma a conclusão.

## Função das portas no FTP

1. **Porta TCP 21 (Conexão de Controle):**
    
    - Responsável pelo envio de comandos do cliente para o servidor e das respostas do servidor para o cliente.
    - Mantém a comunicação contínua e monitora o estado da sessão.
2. **Porta TCP 20 (Conexão de Dados):**
    
    - Exclusiva para a transferência dos dados (arquivos) entre cliente e servidor.
    - Separar o controle dos dados permite que as operações sejam realizadas de forma eficiente e segura.


## Monitoramento do Estado do Usuário

O FTP mantém informações sobre o estado do usuário para garantir uma interação contínua e personalizada. Isso inclui:

- **Autenticação e conta ativa:** Saber qual usuário está autenticado para aplicar permissões específicas.
- **Diretório corrente:** Identificar a localização atual do usuário no sistema de arquivos do servidor, permitindo comandos como `cd` para navegação.


![[Pasted image 20250110170929.png]]

![[Pasted image 20250110171016.png]]