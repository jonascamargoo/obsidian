---
tipo: conceito
area: Redes
tags:
- redes
criada: '2024-10-14'
---

## O que é

Uma [rede de computadores](https://blog.xpeducacao.com.br/rede-mundial-de-computadores/) é composta por uma série de máquinas interligadas. Quando essas máquinas se comunicam, elas compartilham dados, arquivos e informações no geral. Para que essas comunicações ocorram de maneira saudável, segura e funcional, é preciso haver uma estrutura.

A topologia de rede basicamente indica o layout de uma rede de computadores, ou seja, como ela está estruturada. A partir dessa topologia, é possível identificar como as máquinas se conectam e como se comunicam entre si. Existem duas maneiras de representar a estrutura topológica: fisicamente ou logicamente.

## Topologia de rede física Vs Lógica

### Física

A topologia de rede física está relacionada, literalmente, aos elementos físicos que compõem uma rede. Ou seja, ao layout dessa rede. É ela que indica a posição e como estão conectados todos os cabos e dispositivos (máquinas, roteadores e gateways) em um determinado espaço.
Considerando essa definição, é a topologia de rede física que influencia em pontos importantes de uso, como a velocidade e a segurança. Afinal, é a maneira como ela foi estruturada em um ambiente físico que determina o desempenho dessas questões.
### Lógica

Já a topologia de rede lógica está relacionada a como uma rede trabalha, ou seja, como as máquinas interagem entre si e como ocorrem os fluxos de dados através dessa rede.
Diante dessa função, a topologia lógica examina e organiza a rede a fim de encontrar a melhor maneira de conectar seus pontos e garantir um tráfego eficiente.

## Tipos de topologia

Existem 6 tipos de topologia de rede: **anel, árvore, barramento, estrela, híbrida, malha e ponto a ponto**. As 3 principais são Anel, Barramento e Estrela. A topologia híbrida é a mais utilizada atualmente, pois envolve mais de um tipo, como é o caso das duas principais topologias: Estrela/Barramento e Estrela/Switch
### Ponto a Ponto

O formato de rede mais simples é o ponto a ponto. Nele, os nós se conectam entre si, o que faz com que a comunicação entre os dispositivos ocorra rapidamente.

É por conta dessa simplicidade que essa topologia é amplamente aderida nas instalações residenciais. Já em operações mais robustas, que exigem maiores transmissões de dados e infraestrutura, ela não é sustentável.

	![[Pasted image 20240317205147.png]]

### Barramento

A topologia de barramento é um tipo de estrutura de rede em que todos os dispositivos são conectados a um único cabo de transmissão. Nessa configuração, os dados são enviados ao longo do cabo e são recebidos por todos os dispositivos na rede. Não existem dispositivos intermediários, como switches ou roteadores, na topologia de barramento. Mesmo o nome não dê indícios de como sua estrutura é visualmente, a topologia de barramento é uma das mais simples de ser implementada. Neste formato, os dados circulam unilateralmente por meio de um único cabo. Embora tenha um layout simples e econômico, de fácil manutenção, o que é uma grande vantagem, essa estrutura é vulnerável a falhas. Afinal, assim como no caso da topologia de anel, as máquinas estão conectadas em um único fluxo

Principais características da topologia de barramento:

1. **Simplicidade:** A topologia de barramento é simples de configurar e implementar. Requer menos cabos e equipamentos do que outras topologias.
    
2. **Custo:** Devido à sua simplicidade, a topologia de barramento é relativamente barata para ser implantada.
    
3. **Desempenho:** O desempenho da rede pode diminuir à medida que mais dispositivos são adicionados à rede, pois todos os dados devem passar pelo mesmo cabo de transmissão. Além disso, se o cabo de transmissão falhar em qualquer ponto, toda a rede pode ser afetada.
    
4. **Confiabilidade:** A confiabilidade da rede pode ser afetada por falhas no cabo principal, interferências e colisões de dados (quando dois dispositivos tentam transmitir dados simultaneamente).
    
5. **Escalabilidade:** A topologia de barramento pode não ser tão escalável quanto outras topologias, como estrela ou malha, pois adicionar mais dispositivos à rede pode causar congestionamento e degradação do desempenho.
    
6. **Privacidade e segurança:** Como todos os dispositivos compartilham o mesmo cabo de transmissão, não há privacidade nas comunicações. Além disso, a segurança pode ser um problema, já que qualquer dispositivo conectado ao cabo pode "ouvir" todas as comunicações na rede.
    

Apesar de suas limitações, a topologia de barramento ainda é utilizada em algumas redes locais (LANs) de pequeno porte devido à sua simplicidade e baixo custo. No entanto, em redes maiores e mais complexas, outras topologias, como estrela ou malha, são mais comuns devido à sua melhor escalabilidade, desempenho e confiabilidade

#### Características

- Apenas um sinal percorre por vez, ou seja, um [[Conceitos base PCD|nó]] envia informação, ocupando toda a rede. Quando um nó envia o sinal, todos os outros escutam;
- Quando um nó tenta enviar um sinal e o meio está em uso (só pode um por vez), ocorre uma "Colisão". Se há colisão, o nó aguarda o tempo necessário para enviar novamente.
	- E se 2 nós emitirem simultaneamente? O tempo de reenvio de cada nó é aleatório, pois se pré-determinássemos um tempo fixo, a colisão ocorreria novamente entre os mesmo sinais.
- Quem lida com confirmação de recebimento é a camada superior
- Disputa e Colisão são conceitos chave aqui
- Ainda é utilizado em LANs residenciais, redes pequenas...

	![[Pasted image 20240317210041.png]]

### Anel

A topologia de Anel é um tipo de estrutura de rede em que cada dispositivo é conectado ao seu vizinho mais próximo formando um anel fechado. Nesta configuração, os dados circulam em uma única direção ao longo do anel, passando de um dispositivo para o próximo até alcançar o destino desejado.  Há um símbolo (sinal digital) que dá permissão ao nó enviar, evitando disputa e colisões

#### Características

1. **Simplicidade:** A topologia de Anel é relativamente simples de ser implementada e gerenciada. Os dispositivos são conectados em série uns aos outros, formando um circuito fechado.
    
2. **Desempenho:** O desempenho da rede de Anel pode ser consistente, pois não há colisões de dados como na topologia de barramento. Cada dispositivo tem a oportunidade de transmitir seus dados na ordem correta, sem interrupções.
    
3. **Confiabilidade:** A falha de um único dispositivo ou segmento de cabo pode afetar toda a rede. No entanto, algumas topologias de Anel implementam medidas de redundância para contornar esse problema, como Anel Duplo, onde os dados circulam em duas direções opostas, proporcionando caminhos alternativos caso ocorra uma falha.
    
4. **Custo:** A topologia de Anel pode ser mais cara do que a topologia de barramento, pois pode exigir mais cabos e equipamentos para criar o circuito fechado. Além disso, implementar medidas de redundância para aumentar a confiabilidade pode aumentar os custos.
    
5. **Privacidade e segurança:** Como os dados circulam em uma direção específica no Anel, a privacidade das comunicações pode ser melhor do que em topologias onde os dados são transmitidos para todos os dispositivos na rede.
    
6. **Escalabilidade:** A topologia de Anel pode ser menos escalável do que outras topologias, pois adicionar ou remover dispositivos pode interromper temporariamente a operação da rede.
    

A topologia de Anel é comumente utilizada em redes locais (LANs) devido à sua simplicidade e desempenho consistentemente bom. No entanto, em grandes redes, outras topologias como a de estrela ou malha podem ser preferíveis devido à sua maior escalabilidade e confiabilidade. Achavam que seria a rede do futuro, pois não há colisões ou disputas, mas descobriram com o tempo que as disputas e colisões eram menos demoradas que a burocracia desta topologia.

	![[Pasted image 20240317210939.png]]



### Estrela

A topologia estrela é um tipo comum de estrutura de rede em que todos os dispositivos são conectados a um único ponto central, geralmente um dispositivo chamado hub ou switch. Nessa configuração, os dispositivos não estão diretamente conectados entre si, mas sim ao hub central.

#### Características:

1. **Centralização:** A topologia estrela é altamente centralizada em torno do hub ou switch central. Isso facilita a administração, o monitoramento e a resolução de problemas na rede, pois todo o tráfego de dados passa por esse ponto central;
    
2. **Facilidade de instalação e manutenção:** A instalação e a manutenção da topologia estrela são relativamente simples, pois os dispositivos podem ser facilmente conectados ou desconectados do hub central sem afetar os outros dispositivos na rede;
    
3. **Confiabilidade:** A falha de um único dispositivo geralmente não afeta o funcionamento dos outros dispositivos na rede, pois cada dispositivo tem uma conexão direta com o hub central. Isso torna a topologia estrela mais confiável do que algumas outras topologias, como a de barramento, onde uma falha em um ponto pode afetar toda a rede;
    
4. **Desempenho:** O desempenho da topologia estrela pode ser bom, especialmente se o hub ou switch central tiver capacidade suficiente para lidar com o tráfego de dados de todos os dispositivos conectados. No entanto, o desempenho pode ser afetado se muitos dispositivos estiverem transmitindo dados simultaneamente;
    
5. **Privacidade e segurança:** Como os dados não são transmitidos diretamente entre os dispositivos, mas sim através do hub central, a privacidade e a segurança das comunicações podem ser melhoradas, pois é mais difícil para dispositivos não autorizados interceptarem os dados. Ainda assim, assim como na topologia de árvore, o comprometimento do dispositivo central faz com que a rede seja impactada por completo;
    
6. **Custo:** A topologia estrela pode ser mais cara do que algumas outras topologias, pois requer um hub ou switch central e cabos individuais para conectar cada dispositivo a esse ponto central. No entanto, os custos podem ser compensados pela maior confiabilidade e facilidade de gerenciamento.

	![[Pasted image 20240317211700.png]]

A topologia estrela é amplamente utilizada em redes locais (LANs), especialmente em ambientes empresariais e comerciais, devido à sua facilidade de instalação, confiabilidade e capacidade de gerenciamento centralizado. É uma topologia moderna e segura. Há 2 tipos de topologia Estrela: Estrela/Barramento e Estrela/Switch

#### Estrela / Barramento

Nessa configuração, todos os dispositivos são conectados a um hub central (estrela), mas a comunicação entre esses dispositivos é realizada através de um barramento compartilhado. Isso significa que todos os dispositivos compartilham o mesmo meio de transmissão para enviar e receber dados, assim como em uma topologia de barramento. No entanto, a conexão com o hub central é feita de maneira estrelada. Essa configuração combina características de ambas as topologias, estrela e barramento.

- Há disputas e colisões, pois ainda há o barramento interno. Com isso, o desempenho é igual ao do barramento, porém mais organizado, pois ele está embutido.
- Maior quantidade de nós -> maior quantidade de colisões -> menor desempenho


	![[Pasted image 20240317213736.png]]


#### Estrela / Switch

Nessa configuração, todos os dispositivos são conectados a um switch central em vez de um hub. O switch é um dispositivo mais avançado que o hub e tem a capacidade de direcionar o tráfego de dados de forma mais inteligente, transmitindo dados apenas para o dispositivo de destino, em vez de enviar para todos os dispositivos como faz um hub. Isso proporciona um desempenho melhorado e maior eficiência na rede. Essa configuração combina características da topologia estrela com a tecnologia de comutação oferecida pelos switches. Dentro do switch, há um buffer (componente de memória) que enfileira os sinais que ocasionariam colisões. Após estiver livre, o sinal armazenado no buffer é enviado para a porta destinatária sem colidir.


- Redução das disputas e colisões a praticamente 0 (não é 0, pois ainda ocorre no buffer);
- Em função do uso do buffer, o uso para computadores caseiros pode ser menos eficiente, já que as colisões seriam em menor quantidade. Em caso de corporações ou muitos computadores, é mais eficiente que o estrela/barramento.


	![[Pasted image 20240317215028.png]]


### Árvore

A topologia de árvore, também conhecida como hierárquica, é uma combinação das topologias de estrela e barramento. Nessa configuração, os dispositivos são organizados em níveis hierárquicos, semelhantes aos ramos de uma árvore, com um nó central conectado a outros nós secundários e estes, por sua vez, conectados a outros dispositivos.

Principais características da topologia de árvore:

1. **Hierarquia:** A rede é organizada em vários níveis hierárquicos, com um nó central (raiz) conectado aos nós secundários, que, por sua vez, podem estar conectados a outros dispositivos ou sub-redes. Essa estrutura hierárquica facilita a expansão e a escalabilidade da rede.
    
2. **Desempenho:** O desempenho da rede pode ser melhor do que a topologia de barramento, pois as comunicações entre dispositivos não precisam passar por todo o cabo principal. No entanto, o desempenho pode ser afetado se o nó central se tornar um gargalo de tráfego.
    
3. **Confiabilidade:** A topologia de árvore pode oferecer maior confiabilidade do que a topologia de barramento, pois os problemas em um segmento da rede não afetam necessariamente outros segmentos. No entanto, se o nó central falhar, toda a rede pode ser impactada.
    
4. **Custo:** A topologia de árvore pode ser mais cara do que a topologia de barramento, pois requer mais cabos e equipamentos, especialmente se a rede for grande e complexa.
    
5. **Privacidade e segurança:** Como em outras topologias, a privacidade e a segurança dependem das medidas implementadas, como criptografia, firewalls e políticas de acesso. No entanto, a topologia de árvore pode facilitar a implementação de segmentação de rede e controle de acesso em diferentes níveis hierárquicos.

	![[Pasted image 20240317215555.png]]

A topologia de árvore é comumente usada em redes corporativas, institucionais e de telecomunicações, onde é necessário suportar uma grande quantidade de dispositivos distribuídos em vários locais e departamentos. Ela oferece uma estrutura organizada e escalável, que pode acomodar o crescimento e a expansão da rede de forma eficiente.

### Malha

A topologia de malha é um tipo de estrutura de rede em que cada dispositivo está conectado a todos os outros dispositivos na rede, criando assim múltiplos caminhos de comunicação. Nessa configuração, cada dispositivo atua como um nó de roteamento, encaminhando os dados diretamente para o destino ou através de outros dispositivos intermediários.

Principais características da topologia de malha:

1. **Redundância:** A topologia de malha oferece alta redundância, pois há várias rotas alternativas para o tráfego de dados. Se um caminho falhar, os dados podem ser roteados através de outro caminho disponível, garantindo a continuidade da comunicação;
    
2. **Confiabilidade:** Devido à sua redundância, a topologia de malha é altamente confiável. As falhas em um ou mais dispositivos ou links não afetam necessariamente a comunicação, pois ainda existem outros caminhos disponíveis. Esse padrão de organização é vantajoso por sua confiabilidade e, por isso, muitas vezes é usado em grandes operações;
    
3. **Desempenho:** O desempenho da topologia de malha pode ser muito bom, especialmente em redes pequenas ou moderadas, pois permite a distribuição de tráfego e evita congestionamentos em pontos específicos da rede;
    
4. **Privacidade e segurança:** Como os dados são roteados diretamente entre os dispositivos, sem passar por um ponto central, a privacidade e a segurança das comunicações podem ser aprimoradas. No entanto, a implementação de medidas de segurança adicionais, como criptografia, é sempre recomendada;
    
5. **Custo:** A topologia de malha pode ser mais cara do que outras topologias, pois requer uma quantidade maior de cabos e equipamentos para estabelecer todas as conexões entre os dispositivos. No entanto, os custos podem ser compensados pela maior confiabilidade e desempenho;
    
6. **Complexidade:** A configuração e o gerenciamento de uma rede de malha podem ser mais complexos do que outras topologias, especialmente em redes grandes, devido ao grande número de conexões e rotas possíveis.

	![[Pasted image 20240317215839.png]]

A topologia de malha é comumente utilizada em redes de grande porte, como redes de telecomunicações e redes de data centers, onde a confiabilidade e o desempenho são críticos. Também é comum em sistemas de controle industrial e em redes de sensores sem fio, onde a redundância e a tolerância a falhas são essenciais.

### Híbrida

O nome já indica: a topologia de rede híbrida combina mais de um tipo de topologia em sua organização. É por conta dessa versatilidade que hoje é o formato mais utilizado pelo mercado, conseguindo suportar o crescimento das operações.

É essa facilidade de adaptação e consequente redução de custos que gera vantagens à topologia híbrida. Por outro lado, é importante lembrar que a mescla de mais de um tipo de rede gera complexidades na estruturação


	![[Pasted image 20240317215213.png]]