
### **SMTP (Simple Mail Transfer Protocol)**:

1. **Função Principal**: É um protocolo para envio de emails. Ele regula como as mensagens são transmitidas de um remetente para um destinatário através de servidores de correio.
2. **Características**:
    - Usa **TCP** (Transmission Control Protocol) como transporte confiável, normalmente na **porta 25**.
    - Mensagens são limitadas ao formato **ASCII de 7 bits**, refletindo sua origem em 1982.
    - **Servidores intermediários** geralmente não são utilizados; a comunicação é direta entre os servidores de origem e destino.
    - Processo:
        - Um **agente de usuário** envia a mensagem para um **servidor de correio cliente origem**, que coloca a mensagem em uma fila.
        - O **SMTP** transfere a mensagem para o **servidor de correio cliente destino**, onde um agente entrega a mensagem ao destinatário.

### **Comparação com HTTP**:

- **SMTP**: Protocolos para envio. O servidor remetente empurra as informações.
- **HTTP**: Protocolos para recuperação. O servidor responde a solicitações de informações.

### **Protocolos de Recuperação de Mensagens**:

- **POP3 (Post Office Protocol, versão 3)**:
    
    - Simples e com funcionalidades limitadas, usa a **porta 110**.
    - Abre uma conexão TCP para baixar mensagens do servidor e pode marcar mensagens para exclusão.
    - **Limitação**: Não é adequado para usuários nômades (que acessam o email de múltiplos dispositivos ou locais), pois baixa as mensagens e as remove do servidor.
- **IMAP (Internet Message Access Protocol)**:
    
    - Mais complexo, usa a **porta 143**.
    - Permite o armazenamento de mensagens no servidor e acessá-las de diferentes dispositivos.
    - Recursos adicionais:
        - Obter apenas partes da mensagem, como cabeçalhos.
        - Decidir o que fazer download.
    - **Vantagem**: Ideal para redes de baixa velocidade e usuários que acessam de múltiplos locais.

### **Email pela Web**:

- Utiliza navegadores (browsers) e o **HTTP** ou **HTTPS** como protocolos.
    - **HTTP**: Porta **80**.
    - **HTTPS**: Porta **443**.
- Não depende de POP3 ou IMAP para recuperação de mensagens.
- Entre servidores, o envio de mensagens continua utilizando o **SMTP**.

### **Resumo de Portas Importantes**:

1. **SMTP**: Porta **25** (envio de emails).
2. **POP3**: Porta **110** (recuperação básica de emails).
3. **IMAP**: Porta **143** (recuperação avançada de emails).
4. **HTTP**: Porta **80** (acesso à webmail).
5. **HTTPS**: Porta **443** (acesso seguro à webmail).


![[Pasted image 20250110180558.png]]

## Email pela Web 

Usa-se diretamente um browser, sem o uso do POP3 ou IMAP. – HTTP – Porta 80 – HTTPS – Porta 443 – Entre servidores: permanece o SMTP.

### **Exemplo de Envio de Email**

#### **Cenário**:

- Um usuário com email `@gmail.com` deseja enviar uma mensagem para um destinatário com email `@hotmail.com`.

#### **Fluxo**:

1. **Envio Inicial**:
    
    - O usuário `@gmail.com` utiliza seu cliente de email para compor e enviar a mensagem.
    - O cliente faz uma **requisição SMTP** para o **servidor do Gmail**, que recebe a mensagem para processamento.
2. **Transferência entre Servidores**:
    
    - O **servidor do Gmail** utiliza o protocolo **SMTP** para encaminhar a mensagem ao **servidor do Hotmail**, responsável pelo domínio `@hotmail.com`.
3. **Recepção pelo Destinatário**:
    
    - O destinatário `@hotmail.com` utiliza seu cliente de email ou webmail para acessar sua caixa de entrada.
    - O cliente faz uma **requisição ao servidor do Hotmail** (via POP3, IMAP ou diretamente pelo navegador com HTTP/HTTPS) para recuperar a mensagem armazenada no servidor.

---

### **Resumo do Fluxo Técnico**

1. **Cliente Gmail → Servidor Gmail (SMTP)**
2. **Servidor Gmail → Servidor Hotmail (SMTP)**
3. **Cliente Hotmail → Servidor Hotmail (POP3/IMAP/HTTP/HTTPS)**


![[Pasted image 20250110180751.png]]