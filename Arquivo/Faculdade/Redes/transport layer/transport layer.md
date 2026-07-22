---
tipo: conceito
area: Redes
tags:
- redes
criada: '2025-01-23'
---

A camada de transporte oferece suporte aos protocolos que possibilitam a comunicação das aplicações, sendo os principais o TCP e o UDP. O TCP é confiável e orientado à conexão, garantindo a entrega ordenada e sem erros dos dados. É especialmente útil em aplicações onde a integridade das informações é crucial, como transferência de arquivos e serviços de e-mail. Por outro lado, o UDP é mais leve e rápido, mas não fornece garantias de entrega. Ele é amplamente utilizado em aplicações que toleram a perda de pacotes, como streaming de vídeo e áudio em tempo real, onde a velocidade e a baixa latência são mais importantes do que a confiabilidade.

* TCP
	*  Confiável e orientado a conexão (sem erros e na ordem correta);
	* Mecanismo de controle de congestionamento;
	* Limitações na velocidade de transmissão.
* UDP
	* Aplicações em tempo real são tolerantes a perda e não precisam de um transporte totalmente confiável;
	* Não orientado à conexão e não confiável
	* Simples e leve;
	* Muitos firewalls bloqueiam o UDP