
A aule foi introduzida sobre Comparilhamento. Qual a diferença entre comparilhar os seguintes itens?
- processo
- memória
- armazenamento
- dispositivo

Como sistemas operacionais distribuídos conseguem fazer um processo não paralelizavel ser executado de forma paralela (dica: ele faz balanceamento de carga, protelamento, etc)?
## Comparilhamento de memória





### A aula foi introduzida sobre Compartilhamento. Qual a diferença entre compartilhar os seguintes itens?

Em sistemas distribuídos, o "compartilhamento" é um conceito central. Trata-se de permitir que múltiplos processos, possivelmente em máquinas diferentes, acessem ou utilizem um recurso comum. No entanto, a natureza e os desafios desse compartilhamento variam drasticamente dependendo do que está sendo compartilhado.

#### **1. Compartilhamento de Processo**

Compartilhar um processo é um conceito menos comum e mais complexo do que compartilhar outros recursos. Não se trata de múltiplos sistemas executando o mesmo processo simultaneamente, mas sim de mecanismos que permitem a colaboração ou a transferência de processos. As principais formas são:

- **Migração de Processos:** É a capacidade de mover um processo em execução de um nó (computador) para outro na rede. Isso é feito para balanceamento de carga (mover um processo de uma máquina sobrecarregada para uma ociosa) ou para tolerância a falhas (mover um processo de uma máquina que está prestes a falhar). O desafio aqui é transferir todo o estado do processo – registradores da CPU, espaço de endereçamento, arquivos abertos, etc. – de forma transparente.
    
- **Processos Colaborativos:** Em alguns paradigmas, como o de "espaços de tuplas" (Tuple Spaces), múltiplos processos podem cooperar compartilhando dados de forma anônima e assíncrona em um espaço de dados compartilhado, coordenando suas atividades sem comunicação direta.
    

**Diferença chave:** O foco não é o acesso simultâneo ao processo em si, mas sim a **mobilidade** e **coordenação** entre processos no ambiente distribuído.

#### **2. Compartilhamento de Memória**

Este é um dos maiores desafios em sistemas distribuídos. Como os computadores em uma rede possuem memórias físicas separadas, compartilhar memória significa criar uma **abstração** de um único espaço de endereçamento lógico que se estende por toda a rede. Este sistema é conhecido como _Memória Compartilhada Distribuída_ (DSM - Distributed Shared Memory).

- **Como funciona:** Um processo em um nó A pode acessar uma variável que, fisicamente, está na memória do nó B, como se estivesse em sua própria memória local. O sistema operacional distribuído e o middleware são responsáveis por gerenciar o acesso, a transferência de dados (geralmente em páginas de memória) e, crucialmente, a consistência dos dados entre os nós.
    

**Diferença chave:** Cria a **ilusão de um hardware de memória compartilhada (multiprocessador)** em um ambiente de hardware com memória privada (multicomputador), simplificando a programação, mas introduzindo complexos problemas de consistência.

#### **3. Compartilhamento de Armazenamento**

Este é o tipo de compartilhamento mais comum e visível para os usuários. Ele é realizado através de _Sistemas de Arquivos Distribuídos_ (DFS - Distributed File Systems), como NFS (Network File System) ou HDFS (Hadoop Distributed File System).

- **Como funciona:** Arquivos e diretórios localizados fisicamente em um ou mais servidores de armazenamento são acessíveis por múltiplos clientes na rede como se estivessem em seus discos locais. O sistema gerencia o acesso, o controle de concorrência (garantindo que dois usuários não corrompam o mesmo arquivo ao editá-lo simultaneamente), a segurança e a replicação para tolerância a falhas.
    

**Diferença chave:** O foco é o compartilhamento de **dados persistentes (arquivos)** de forma transparente e robusta, abstraindo a localização física do armazenamento.

#### **4. Compartilhamento de Dispositivo**

Refere-se a tornar um dispositivo de hardware, conectado a um nó específico, acessível a outros nós na rede. O exemplo clássico é a impressora de rede.

- **Como funciona:** Um computador ao qual a impressora está conectada atua como um "servidor de impressão". Outros computadores enviam seus trabalhos de impressão para este servidor, que gerencia uma fila e envia os trabalhos para a impressora um de cada vez. O mesmo princípio se aplica a scanners, plotters, e até mesmo hardware especializado (como GPUs potentes para processamento remoto).
    

**Diferença chave:** Permite que **recursos de hardware periféricos** caros ou específicos sejam utilizados por toda a rede, otimizando custos e acesso.

---

### Como sistemas operacionais distribuídos conseguem fazer um processo não paralelizável ser executado de forma paralela?

Esta é uma excelente pergunta que toca numa distinção crucial. Um processo que é inerentemente sequencial (não paralelizável) **não pode ter suas instruções internas executadas em paralelo**. Se a instrução `B` depende do resultado da instrução `A`, elas devem, por definição, ser executadas em ordem.

O que um sistema operacional distribuído faz não é quebrar a lógica sequencial de _um_ processo, mas sim gerenciar a execução de _múltiplos processos_ (que podem ser sequenciais) de forma concorrente em diferentes nós do sistema. O objetivo é alcançar o **paralelismo no nível do sistema (throughput)**, não no nível de um único processo.

As técnicas mencionadas na dica são os mecanismos para atingir esse objetivo:

1. **Balanceamento de Carga (Load Balancing):** Imagine uma fila de processos esperando para serem executados. Em vez de todos executarem em um único supercomputador, um balanceador de carga distribui esses processos entre vários computadores (nós) disponíveis na rede. Se um nó está ocioso e outro está sobrecarregado, o sistema pode alocar o próximo processo para o nó ocioso. Isso garante que nenhum nó se torne um gargalo e que os recursos do sistema como um todo sejam utilizados de forma eficiente.
    
2. **Protelamento (Escalonamento):** O termo mais técnico seria **escalonamento (scheduling)**. O sistema operacional distribuído possui um escalonador global que decide não apenas _quando_ um processo deve ser executado, mas também _onde_ (em qual nó). Essa decisão pode se basear em vários fatores: carga atual de cada nó, local dos dados que o processo precisa acessar (para minimizar a comunicação de rede), capacidades de hardware específicas de cada nó, etc.
    
3. **Migração de Processos (mencionada anteriormente):** Esta é a ferramenta que torna o balanceamento de carga dinâmico. Se um processo já está em execução em um nó que subitamente se torna sobrecarregado (por exemplo, porque outros processos mais pesados foram iniciados nele), o sistema pode pausar o processo, transferir todo o seu estado para um nó menos carregado e continuar sua execução lá. Para o usuário e para o próprio processo, essa migração é, idealmente, transparente.
    

**Em resumo:** O sistema não executa um processo sequencial em paralelo. Ele executa uma **carga de trabalho** composta por muitos processos de forma paralela, distribuindo-os inteligentemente pelos recursos disponíveis para maximizar a vazão e a eficiência geral do sistema.

---

## Compartilhamento de Memória

Como visto, o compartilhamento de memória em um sistema distribuído é sobre criar a abstração de um espaço de endereçamento global e compartilhado em um sistema onde a memória é fisicamente distribuída. Essa abstração é chamada de **Memória Compartilhada Distribuída (DSM)**.

**O Objetivo:** Simplificar a programação. Para um programador, é muito mais intuitivo e simples ler e escrever em uma variável compartilhada do que ter que implementar explicitamente a troca de mensagens (enviar e receber pacotes de dados) para sincronizar informações entre processos em máquinas diferentes.

**O Grande Desafio: Consistência de Memória**

O problema fundamental da DSM é garantir que todos os nós tenham uma visão consistente da memória. Considere o seguinte cenário:

1. O nó `A` lê o valor da variável `x` (que é 5) de uma página de memória compartilhada.
    
2. O nó `B` também lê o valor de `x` (5).
    
3. O nó `A` atualiza `x` para 10.
    
4. Agora, o nó `B` tenta ler `x` novamente. Qual valor ele deve ver? 5 ou 10?
    

Se o sistema não propagar a atualização de `A` para `B` antes da leitura de `B`, os nós terão uma visão inconsistente da memória, levando a bugs e comportamento incorreto do programa.

Para resolver isso, foram criados vários **Modelos de Consistência**, que são como "contratos" que o sistema de memória oferece ao programador, definindo as regras sobre quão desatualizado um valor de memória pode estar. Alguns exemplos (do mais forte para o mais fraco) são:

- **Consistência Estrita:** A mais forte e intuitiva. Qualquer leitura a uma posição de memória `x` retorna o valor da escrita mais recente em `x`. É quase impossível de implementar em um sistema distribuído real devido à latência da rede.
    
- **Consistência Sequencial:** O resultado de qualquer execução é o mesmo como se as operações de todos os processadores fossem executadas em alguma ordem sequencial, e as operações de cada processador individual aparecem nesta sequência na ordem especificada por seu programa. É mais relaxada, mas ainda garante um comportamento que faz sentido logicamente.
    
- **Consistência Causal:** Garante que operações que são causalmente relacionadas sejam vistas por todos os processos na mesma ordem. Operações concorrentes (não relacionadas) podem ser vistas em ordens diferentes por processos diferentes.
    

A implementação da DSM geralmente envolve o sistema operacional interceptando acessos à memória. Quando um processo tenta acessar uma página de memória que não está localmente, ocorre uma falha de página (_page fault_). O SO então se comunica pela rede para buscar a página do nó que a possui, ao mesmo tempo em que invalida ou atualiza cópias antigas em outros nós para manter o modelo de consistência escolhido.



Excelente pergunta! A frase do seu professor é uma daquelas afirmações que parecem contraditórias, mas que escondem uma verdade fundamental sobre a arquitetura de sistemas distribuídos. E a sua intuição sobre "não existir paralelismo de memória" está no caminho certo.

Vamos quebrar tudo isso em partes.

### Explicando a Frase do Professor

A afirmação: _"o sistema operacional distribuído consegue compartilhar processos, mas não memória, pois o computador distante não consegue descobrir o tamanho do objeto"._

Aqui, a palavra "compartilhar" está sendo usada de duas maneiras diferentes, e essa é a chave para entender.

#### 1. "Compartilhar" Processos (via Migração)

Quando o professor diz que um SO distribuído pode "compartilhar processos", ele se refere principalmente à **migração de processos**.

- **O que é?** É a capacidade de pausar um processo em execução na Máquina A, empacotar todo o seu estado (registradores da CPU, pilha, dados, etc.), enviá-lo pela rede e continuar sua execução na Máquina B.
    
- **Por que isso é "compartilhar"?** Porque o processo não está preso a um único hardware. O _pool_ de recursos computacionais de todo o sistema distribuído está disponível para ele. O sistema pode mover o processo para uma máquina com mais carga livre (balanceamento de carga) ou para longe de uma máquina que está prestes a falhar.
    
- **Como isso é possível?** É extremamente complexo, mas é um problema "contido". O SO na Máquina A sabe tudo sobre o processo: sabe o tamanho de sua memória alocada, quais arquivos ele abriu, etc. Ele pode reunir todas essas informações em um pacote e enviá-lo. A Máquina B recebe esse pacote e o "desempacota", recriando o estado do processo.
    

#### 2. Por que "não se pode compartilhar" Memória?

Aqui está o ponto crucial da frase. Não se trata de ser impossível criar uma _abstração_ de memória compartilhada (como a DSM que discutimos), mas sim de que **não existe compartilhamento de memória _físico e nativo_** entre computadores diferentes.

Pense em um único computador com um processador multi-core. Todos os núcleos têm acesso direto e físico à mesma placa de memória RAM. O hardware e o sistema operacional têm um mapa unificado e perfeito de todo o espaço de endereçamento.

Agora, considere duas máquinas em uma rede:

- **Espaços de Endereçamento Separados:** A Máquina A tem sua própria RAM, com seus próprios endereços físicos. A Máquina B tem a sua. O endereço de memória `0x1000` na Máquina A não tem absolutamente nenhuma relação com o endereço `0x1000` na Máquina B.
    
- **O Problema do "Tamanho do Objeto":** Essa é a consequência direta do ponto anterior. Se um programa na Máquina A cria um objeto (uma struct, uma classe, um array) na sua memória, a Máquina B não tem como "olhar" para a memória da Máquina A e saber que naquele endereço existe um objeto e que ele ocupa, digamos, 50 bytes. Essa informação simplesmente não existe em seu hardware ou em seu mapa de memória.
    

A sua resposta está correta e muito perspicaz: **"não existe paralelismo de memória"** no sentido físico. Para que a Máquina B saiba qualquer coisa sobre um objeto na Máquina A, a Máquina A precisa **explicitamente enviar uma mensagem** pela rede contendo os dados desse objeto.

O que você pode fazer, como mencionou, é criar um **Sistema de Memória Compartilhada Distribuída (DSM)**. Mas isso é uma **camada de software (uma abstração)** que _simula_ a memória compartilhada. Ele funciona interceptando acessos à memória e traduzindo-os em mensagens de rede para buscar ou atualizar dados em outras máquinas. É lento, complexo e cheio de desafios de consistência, precisamente porque o hardware subjacente não oferece suporte nativo.

**Resumo da Frase:** Podemos mover um processo inteiro (que é uma entidade bem definida pelo SO local), mas não podemos fazer com que duas máquinas tratem seus pools de RAM separados como se fossem um só, porque o hardware não permite essa visão unificada e direta.

---

Grid -> memória compartilhada nativamente
Cluster -> processos compartilhados nativamente (precisando de um middlewere)

Em pesquisas climatológicas utilizam grids (geralmente free bsd com kernel alterado para o volume específico de memória e processadores)



TRABALHO 1

Ele está mais interessado em como o client e servidor são conectados (parte transacional entre cliente e servidor)

Fazer o chapter solution que o leo postou


Qual a diferneça entre SDR, SOR? sei que o SOR garante o desempenho e o SDR garante a disponibilidade, já a rede garante a confiabilidade. Só pra esclarecer, as camadas são SDR  -> middlewhere -> SOR -> Rede, do alto nível para o baixo.


