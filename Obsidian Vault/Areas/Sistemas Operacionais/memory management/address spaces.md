## Troca de processos (Swapping) - não atende aos dias de hoje, rara utilização

O **swapping de processos** é uma técnica de gerenciamento de memória que envolve mover processos entre a memória principal e o disco para otimizar o uso de recursos. No início, apenas um processo (como o A) pode estar na memória. À medida que novos processos (B e C) são criados ou trazidos do disco, eles ocupam mais espaço na memória. Quando a memória fica cheia, processos podem ser movidos de volta para o disco (swap out), liberando espaço para outros, como o processo D. Quando um processo retorna à memória (swap in), ele pode ser carregado em uma posição diferente, exigindo a realocação de seus endereços, tarefa geralmente realizada pelo hardware, com o uso de registradores base e limite - registradores base e limite são responsáveis por demarcar o início e fim do endereço, possibilitando a mágica do **endereçamento de memória**.

### Fragmentação de memória

O swapping pode criar fragmentação na memória, com espaços livres espalhados. Para consolidar esses espaços, pode-se utilizar a **compactação de memória**, que move os processos para baixo, criando um bloco contínuo de memória livre. Contudo, essa técnica consome muito tempo de CPU e raramente é usada. Por exemplo, compactar a memória de uma máquina de 16 GB poderia levar cerca de 16 segundos.


![[Pasted image 20250114171202.png]]

### Alocação de memória

Quando processos têm tamanhos fixos, o sistema operacional pode alocar exatamente o espaço necessário. No entanto, se os processos precisam crescer dinamicamente (como em linguagens que permitem alocação e liberação de memória), surgem complicações. Se houver espaço adjacente ao processo, ele pode expandir; caso contrário, ele precisará ser movido para outro local com espaço suficiente, ou outros processos terão que ser trocados para liberar memória. Em situações extremas, se a memória ou o disco estiverem cheios, o processo pode ser suspenso ou até encerrado.

Para processos que tendem a crescer, é útil alocar memória extra no momento da troca ou movimentação, reduzindo a frequência de operações de realocação. No entanto, ao transferir processos para o disco, apenas a memória realmente utilizada deve ser movida, evitando desperdício.

Alguns sistemas utilizam uma abordagem em que processos têm dois segmentos em expansão: um para dados e outro para a pilha. Nesse modelo, o segmento de dados cresce para cima e a pilha cresce para baixo, compartilhando a memória entre eles. Caso o espaço disponível entre os segmentos se esgote, o processo pode ser movido para outra área com mais espaço, enviado ao disco, ou encerrado. Essa estratégia permite maior flexibilidade, mas também exige gerenciamento eficiente para evitar interrupções no sistema.

![[Pasted image 20250114171229.png]]


## Nos dias atuais...

Como consequência desses desenvolvimentos, há uma necessidade de executar programas que são grandes demais para se encaixar na memória e há certamente uma necessidade de ter sistemas que possam dar suporte a múltiplos programas executando em simultâneo, cada um deles encaixando-se na memória, mas com todos coletivamente excedendo-a. A troca de processos não é uma opção atraente, visto que o disco SATA típico tem um pico de taxa de transferência de várias centenas de MB/s, o que significa que demora segundos para retirar um programa de 1 GB e o mesmo para carregar um programa de 1 GB. Podemos dizer que cerca de 99% desse trabalho não é feito por swapping e sim por **memória virtual**.

Embora o trabalho real de troca de sobreposições do disco para a memória e vice-versa fosse feito pelo sistema operacional, o trabalho da divisão do programa em módulos tinha de ser feito manualmente pelo programador. Dividir programas grandes em módulos pequenos era uma tarefa cansativa, chata e propensa a erros. Poucos programadores eram bons nisso. Não levou muito tempo para alguém pensar em passar todo o trabalho para o computador.

