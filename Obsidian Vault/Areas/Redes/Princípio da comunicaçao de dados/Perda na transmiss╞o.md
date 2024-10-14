
Os meios de transmissão não são perfeitos, portanto, perda de sinal acontece. Ou seja, o sinal enviado não é o mesmo recebido. Causas da perda: Atenuação, distorção e ruído

## Atenuação

A atenuação é um tipo comum de perda na transmissão que ocorre devido à redução da energia do sinal ao viajar através do meio de comunicação. Essa perda de energia ocorre principalmente devido à resistência do meio de transmissão e a outros efeitos físicos, como dispersão e reflexão. Podemos compensar a perda com o uso de amplificadores, que são objetos usados para aumentar o nível de energia do sinal, permitindo o sinal alcançar distâncias maiores. O decibel (dB) é uma unidade de medida usada para expressar a relação entre duas potências ou intensidades de sinais, em dois pontos diferentes da transmissão. A fórmula básica para calcular o ganho ou perda em decibéis é: 

$$ dB = 10 \times \log_{10} \left( \frac{P2}{P1} \right) $$

onde P1 e P2 são as potências do sinal nos pontos 1 e 2, respectivamente

#### Exemplos

1 - Um sinal trafega por um meio de transmissão e sua potência é reduzida pela metade. Qual foi a perda de potência (atenuação)?

$$
P2 = \frac{P1}{2}
$$

$$
10 \log_{10} \left( \frac{P2}{P1} \right) = 10 \log_{10} \left( \frac{0,5P1}{P1} \right) = 10 \log_{10} (0,5) = -3 \, \text{dB}
$$

2 - Um sinal passa por amplificador e sua potência é aumentada em 10 vezes. Qual foi o ganho de potência (amplificação)?

$$
P2 = 10P1
$$

$$
10 \log_{10} \left( \frac{P2}{P1} \right) = 10 \log_{10} \left( \frac{10P1}{P1} \right) = 10 \log_{10} (10) = 10 \, \text{dB}
$$



### Tipos de atenuação

#### Reflexão
Ocorre quando uma onda eletromagnética atinge um obstáculo, que tem dimensões muito maiores que o comprimento da onda do sinal, fazendo com que o sinal mude de direção. Parte do sinal pode ser refletida de volta, reduzindo a potência do sinal que segue na direção original.

	![[Pasted image 20240729135644.png]]

#### Difração
A difração é a alteração da direção de propagação de um sinal quando ele encontra um obstáculo ou passa por uma abertura. Isso pode causar a dispersão do sinal e reduzir sua intensidade.

	![[Pasted image 20240729134829.png]]

#### Espalhamento (Scattering)
O espalhamento ocorre quando o sinal é desviado em várias direções devido a irregularidades ou partículas no meio de transmissão. Isso resulta na redução da potência do sinal original.

	![[Pasted image 20240729135307.png]]

#### Dispersão
A dispersão é o fenômeno onde diferentes componentes do sinal viajam a diferentes velocidades, resultando na separação do sinal ao longo do tempo ou da distância. Isso pode causar a atenuação da qualidade do sinal.



#### Refração

A refração é a mudança de direção de um sinal ao passar de um meio para outro com densidades diferentes. Essa mudança pode causar a atenuação do sinal, pois parte da energia do sinal pode ser perdida.

## Distorção

Distorção significa que o sinal muda sua forma ou seu formato. Pode acontecer em um sinal composto. 
Cada componente do sinal tem sua própria velocidade de propagação em um meio e, portando, seu próprio retardo em atingir o destino final.

## Ruído

Ruído é qualquer sinal indesejado que interfere na transmissão e recepção de dados em um sistema de comunicação. Ele pode distorcer ou mascarar o sinal útil, reduzindo a qualidade da comunicação.

Pode ser encontrado nas seguintes formas:

- Térmico: movimentação aleatória de elétrons em um cabo que provoca um sinal extra que não foi enviado pelo transmissor;
- Induzido: provém de motores e aparelhos elétricos. Os aparelhos atuam como antena transmissora e o cabo como uma antena receptora;
- Impulso: é um pico, sinal com grande energia e em curto espaço de tempo, provocado por descargas atmosféricas ou cabo de energia;
- Linha cruzada: efeito de um fio sobre o outro.
- Não acontece no digital, apenas no analógico. Por ser contínuo, escuta tudo entre a crista e o vale. Qualquer ruído é interpretado pelo receptor.

### Relação sinal/ruído (SNR)

Para determinar o limite teórico da taxa de transferência, é fundamental compreender a relação entre a potência do sinal e a potência do ruído. Essa relação é expressa pela Relação Sinal-Ruído (SNR), calculada como a razão entre a potência média do sinal e a potência média do ruído -> SNR=(potência do sinal / 0) = infinito.

A relação sinal-ruído compara o nível de um sinal desejado com o nível do ruído de fundo. Quanto mais alta for a relação sinal-ruído, menor é o efeito do ruído de fundo sobre a detecção ou medição do sinal.




