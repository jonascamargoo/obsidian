---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-14'
---

## O que é?

Bluetooth é uma tecnologia de comunicação sem fio de curto alcance que permite a transferência de dados entre dispositivos eletrônicos, como smartphones, computadores, alto-falantes, fones de ouvido, teclados e outros dispositivos habilitados para Bluetooth. Utilizando ondas de rádio na faixa de frequência de 2,4 GHz, o Bluetooth permite a conexão e a troca de informações de forma rápida e conveniente, geralmente em um raio de até 10 metros, dependendo da classe do dispositivo. Essa tecnologia é amplamente empregada em dispositivos móveis e periféricos, possibilitando a transmissão de áudio, vídeo, dados e comandos de controle de maneira sem fio, facilitando a interconexão e a integração entre diferentes dispositivos eletrônicos.

É composta por uma piconet, do tipo  [Ad-Hoc](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FRedes%2FPrinc%C3%ADpio%20da%20comunica%C3%A7ao%20de%20dados%2FWireless%2FAd-Hoc).

- Automatização de componentes eletrônicos em um escritório, residência, veículo...
- Ad-Hoc: não precisa de um dispositivo central
- PnP (plug and play): não precisa ser configurada, apenas autorizada
- Composição:
	-  Piconet -> 8 dispositivos, sendo 1 mestre e 7 escravos
	![[Pasted image 20240317180910.png]]


## Piconet

Uma **piconet** é uma pequena rede de dispositivos conectados via Bluetooth. Em uma piconet, há uma configuração hierárquica onde um dispositivo atua como o **mestre** e os outros dispositivos conectados a ele são chamados de **escravos**.

### Definição de Termos

1. **Mestre (Master)**:
    
    - O dispositivo que inicia a comunicação e gerencia a rede.
    - Controla a sincronização da rede, atribuindo tempos de transmissão para cada dispositivo.
    - Pode se conectar a até sete dispositivos escravos ativos simultaneamente.
2. **Escravo (Slave)**:
    
    - Dispositivo que responde às solicitações do mestre.
    - Segue a sincronização e as regras definidas pelo mestre.
    - Pode existir em número de até 255 na rede, mas apenas sete podem ser ativos ao mesmo tempo, os demais permanecem em modo de espera (parked).

### Funcionamento da Piconet

1. **Formação**:
    
    - Um dispositivo (mestre) inicia a piconet enviando sinais de conexão.
    - Dispositivos dentro do alcance (escravos) respondem e solicitam para se conectar.
2. **Comunicação**:
    
    - O mestre controla a comunicação, atribuindo intervalos de tempo para cada escravo enviar ou receber dados.
    - Escravos só transmitem dados quando solicitados pelo mestre.
3. **Sincronização**:
    
    - O mestre mantém a sincronização da rede através de seu relógio interno, que todos os escravos seguem.
4. **Gestão de Dispositivos**:
    
    - O mestre pode adicionar ou remover escravos da piconet conforme necessário.
    - Escravos podem ser colocados em diferentes estados (ativo, em espera, ou em modo de espera) pelo mestre.