---
tipo: conceito
area: Sistemas Distribuidos
tags:
- dev/sistemas-distribuidos
criada: '2024-10-14'
---

Foco: _interface e comunicação remota entre processos heterogêneos_.

Considere a lógica do escalonamento de processos de Sistemas operacionais, com seu devio processo e devidas trocas de mensagens. Vamos discutir o do RPC (remote procedure call). RPC consiste em passar essa informação via rede para outra máquina, basicamente conseguir comunicar o escalonamento dos processos de cada máquina para a outra máquina daquela rede. No nosso caso, não utilizaremos middlewhere, a linguagem deve fazer isso sem middlewhere. Como faremos isso sem middlewhere, caso, por exemplo, na máquina um estivemos falando de código java e no dois com código python (ambos com assembly diferente). Relembrando que cada código está em espaço de memória exclusivo (a máquina 1 não tem conhecimento da memória da máquina 2). A "Interface" de IDL é a interface entre os Procedures.

Exemplos de IDLs: WSDL, JSON-WSL, JNI


CódigoA {
	- espaço memória exclusiva
	- programa de tratamento de dados
	- send
	- receive

}

CódigoB {
	- mem Exec'
	- Programa'
	- Send'
	- Receive'
}



Como aqui não temos middlewhere, então precisamos nos preocupar se a mensagem chegou de fato, se foi de fato enviada, utilizando os senders e receivers.