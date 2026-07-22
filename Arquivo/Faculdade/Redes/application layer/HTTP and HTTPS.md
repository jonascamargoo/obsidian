---
tipo: conceito
area: Redes
tags:
- redes
criada: '2025-01-10'
---

O HTTP (Hypertext Transfer Protocol) é o protocolo base para a transferência de páginas web. Ele opera de maneira simples, solicitando e enviando objetos como texto, imagens e vídeos. Contudo, é um protocolo stateless, o que significa que ele não mantém informações sobre conexões anteriores, tornando-o menos eficiente em certas aplicações. Já o HTTPS (HTTP Secure) é uma versão segura do HTTP, que adiciona uma camada de criptografia às comunicações. Essa criptografia garante a confidencialidade e a integridade dos dados transmitidos, protegendo contra interceptações e ataques de terceiros. A principal diferença técnica entre eles está no uso de certificados digitais e da porta 443 para o HTTPS, enquanto o HTTP utiliza a porta 80.



![[Pasted image 20250110155806.png]]

OBS: não persiste, é feito em memória, diferente da FTP, que grava o arquivo



![[Pasted image 20250110162303.png]]

Nas versões mais novas (persistente), o servidor deixa a conexão TCP aberta após a resposta. Fecha quando não é usada por um determinado tempo.


## Diferenças

* As URLs HTTPS começam com "https://" e utilizam a porta 443 como padrão, enquanto as URLs HTTP começam com "http://" e utilizam a porta 80 como padrão.;

*  HTTP é inseguro e sujeito a ataques de homem-no-meio e escutas ilegais, que podem levar a atacantes ganharem acesso a contas de páginas na web e a informações sensíveis.;

* O HTTPS foi projetado para proteger contra esses ataques e é considerado seguro contra eles (com exceção de versões mais antigas e obsoletas do SSL).



