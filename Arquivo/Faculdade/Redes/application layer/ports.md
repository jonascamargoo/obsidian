---
tipo: conceito
area: Redes
tags:
- redes
criada: '2025-01-10'
---

## O que são portas?

Em redes de computadores, uma **porta** é um número lógico usado para identificar serviços ou processos específicos em um dispositivo conectado à rede. As portas permitem que várias aplicações em execução em um mesmo computador possam enviar e receber dados simultaneamente, diferenciando os dados que chegam e saem com base no número da porta.

Cada porta é identificada por um número que varia de **0 a 65.535** e funciona como um ponto de entrada ou saída para a comunicação de rede. Por exemplo:

- **Porta 80:** Usada pelo protocolo HTTP.
- **Porta 443:** Usada pelo protocolo HTTPS.
- **Porta 25:** Usada pelo protocolo SMTP para envio de e-mails.

As portas são um componente essencial dos **sockets**, que combinam o endereço IP do dispositivo e o número da porta para criar um canal exclusivo de comunicação.

| Aplicações               | Protocolo na camada de aplicação | Protocolo na camada de transporte |
|---------------------------|----------------------------------|------------------------------------|
| Correio eletrônico        | SMTP, POP3, IMAP, HTTP          | TCP                                |
| Acesso a terminal         | Telnet                          | TCP                                |
| Web                       | HTTP                            | TCP                                |
| Transferência de arquivo  | FTP                             | TCP                                |
| Multimídia em tempo real  | HTTP, RPT                       | UDP ou TCP                         |
| Telefonia por Internet    | SIP, RPT                        | UDP                                |
### Portas UDP/TCP

16 bits = 65.536
*  até 1024 - portas conhecidas, controladas pelo IANA;
* ftp: 21 e 20
* ssh: 22
* telnet: 23
* http: 80
* https: 443
* smtp: 25
* dns: 53
* pop3: 110
* imanp: 143
* Snmp: 161 e 162
