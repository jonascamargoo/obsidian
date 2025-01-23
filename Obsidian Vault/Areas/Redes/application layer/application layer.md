## O que é?

A camada de aplicação no modelo de redes [TCP](obsidian://open?vault=obsidian&file=Obsidian%20Vault%2FAreas%2FRedes%2Ftransport%20layer%2Ftransport%20layer)/[IP](obsidian://open?vault=obsidian&file=Obsidian%20Vault%2FAreas%2FRedes%2Fnetwork%20layer%2Fnetwork%20layer) é onde ocorre a interação entre os usuários e a rede, proporcionando os serviços necessários para as aplicações que utilizamos diariamente, como navegação na web, envio de e-mails e compartilhamento de arquivos. Essa camada atua como um ponto de entrada para os dados, traduzindo solicitações e respostas para que possam ser compreendidas pelos usuários e pela infraestrutura de rede. Sua relevância está no fato de que ela abrange os protocolos que tornam possíveis serviços essenciais, como HTTP, FTP e SMTP, além de permitir a comunicação entre sistemas heterogêneos.

## Arquitetura de aplicação

Existem dois modelos principais de arquiteturas na camada de aplicação: cliente/servidor e peer-to-peer (P2P):

### client/server

Na arquitetura cliente/servidor, o servidor desempenha um papel central e está sempre ativo, geralmente configurado com um endereço IP fixo. Ele atende às solicitações feitas pelos clientes, que podem ser navegadores, softwares de e-mail ou outros programas. Essa abordagem é amplamente utilizada em aplicações como a web, comércio eletrônico e redes sociais, onde a confiabilidade e o controle centralizado são prioritários.

* Hospedeiro (servidor) sempre em funcionamento;
* Servidor com endereço IP fixo;
* [HTTP](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FRedes%2Fapplication%20layer%2FHTTP%20and%20HTTPS), [FTP](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FRedes%2Fapplication%20layer%2FFTP), [SSH](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FRedes%2Fapplication%20layer%2FSSH) ,[ SMTP](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FRedes%2Fapplication%20layer%2FSMTP);
* Servidor virtual: grande número de hospedeiros para atender requisições dos clientes;
* Mecanismo de busca (Google), yt, amazon...

### P2P

Por outro lado, a arquitetura peer-to-peer elimina a necessidade de um servidor fixo, permitindo que os pares (hospedeiros) se comuniquem diretamente. Essa abordagem descentralizada é mais econômica e escalável, pois cada novo par contribui com recursos ao sistema. No entanto, a segurança é um desafio maior nesse modelo. Exemplos notáveis de aplicações P2P incluem o BitTorrent para compartilhamento de arquivos e o Skype para telefonia via internet.

*  Confiança mínima entre os servidores;
*  Comunicação direta entre hospedeiros (pares);
* Hospedeiros controlados por usuários;
* Distribuição de arquivos (BitTorrent), compartilhamento de arquivos (eMule, LimeWire), telefonia (Skype), IPTV (PPLive);
* Autoescalabilidade: cada par acrescenta capacidade de serviço ao sistema;
* Baixo custo: não requer grande infraestrutura de serviço e largura de banda;
* A maioria dimensionada para largura de banda assimétrica (xDSL e MAN a cabo);
* Depende de usuários participativos em oferecer largura de banda, armazenamento e recursos de computação para as aplicações



