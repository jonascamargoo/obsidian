## O que é?

O algoritmo CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance) é um protocolo de controle de acesso ao meio usado em redes de comunicação sem fio, como as redes IEEE 802.11 (Wi-Fi). Ele foi projetado para minimizar colisões de dados e aumentar a eficiência da comunicação em redes onde múltiplos dispositivos compartilham o mesmo canal de comunicação.

	![[Pasted image 20240729132345.png]]

## Funcionamento do CSMA/CA

1. **Sense the Carrier (Sentir o Canal)**:
    
    - Antes de transmitir dados, um dispositivo (nó) verifica o canal para determinar se ele está ocupado ou livre. Isso é feito ouvindo o canal por um período de tempo específico.
2. **If Channel is Idle (Se o Canal Estiver Livre)**:
    
    - Se o canal estiver livre, o dispositivo pode iniciar a transmissão dos dados.
3. **If Channel is Busy (Se o Canal Estiver Ocupado)**:
    
    - Se o canal estiver ocupado, o dispositivo espera um período de tempo aleatório antes de verificar novamente se o canal está livre. Esse período de espera é conhecido como "backoff" e ajuda a evitar colisões subsequentes.
4. **Collision Avoidance (Evitação de Colisões)**:
    
    - Para reduzir a probabilidade de colisões, o CSMA/CA usa um mecanismo de espera aleatória (random backoff). Cada dispositivo seleciona aleatoriamente um intervalo de tempo para esperar antes de tentar transmitir novamente. Isso ajuda a evitar que vários dispositivos tentem transmitir ao mesmo tempo após o canal ficar livre.
5. **RTS/CTS (Request to Send/Clear to Send)**:
    
    - Em redes Wi-Fi, pode ser utilizado um mecanismo adicional de controle de colisões chamado RTS/CTS. Antes de enviar dados, um dispositivo envia um quadro RTS (Request to Send) ao destinatário. O destinatário responde com um quadro CTS (Clear to Send) se o canal estiver livre. Isso reserva o canal para a transmissão, reduzindo a probabilidade de colisões, especialmente em ambientes com alta densidade de dispositivos.


## Vantagens e desvantagens
### Vantagens do CSMA/CA

- **Redução de Colisões**: A espera aleatória (backoff) e o uso de RTS/CTS ajudam a reduzir colisões de dados, melhorando a eficiência da rede.
- **Adaptabilidade**: CSMA/CA é eficaz em ambientes dinâmicos onde a quantidade de dispositivos e o tráfego podem variar significativamente.
- **Simplicidade**: O protocolo é relativamente simples de implementar e não requer sincronização complexa entre dispositivos.

### Desvantagens do CSMA/CA

- **Overhead de Controle**: O uso de RTS/CTS adiciona overhead à comunicação, o que pode reduzir a largura de banda disponível para dados.
- **Latência**: A espera aleatória (backoff) pode introduzir latência adicional na comunicação, especialmente em redes congestionadas.
- **Hidden Node Problem**: Em redes Wi-Fi, dispositivos que estão fora do alcance um do outro (nós ocultos) podem não detectar transmissões mútuas, levando a colisões.


## Repetidores de sinal

O uso de repetidores de sinal (com AP), é desencorajado exatamente por causa do funcionamento desse algoritmo. O backoff é duplo nesse caso.