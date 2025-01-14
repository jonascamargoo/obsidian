
## O que é um processo?

Um processo é basicamente uma **instância de um programa em execução**. Esse programa contém uma série de instruções, e o processo é a execução real dessas instruções. Em outras palavras, **um processo é um programa em ação**.  Podemos definir um processo como um container com todos os recursos necessários para um programa funcionar (processo é sobre agrupar recursos).

Ao iniciarmos aplicativos como o **navegador**, **IDE**, **agentes**, **aplicações**, **bancos de dados** e outros serviços, o sistema operacional cria um processo para cada um desses programas, fornecendo os recursos necessários para sua execução. Isso inclui **espaço de memória isolado**, **threads**, **contextos** e a gestão do **próprio ciclo de vida** do processo.  Conceitualmente, cada processo tem sua própria CPU virtual.

## Processo vs Programa

A diferença entre um processo e um programa é sutil, mas absolutamente crucial. Uma analogia poderá ajudá-lo aqui: considere um cientista de computação que gosta de cozinhar e está preparando um bolo de aniversário para sua filha mais nova. Ele tem uma receita de um bolo de aniversário e uma cozinha bem estocada com todas as provisões: farinha, ovos, açúcar, extrato de baunilha etc. Nessa analogia, a receita é o programa, isto é, o algoritmo expresso em uma notação adequada, o cientista de computação é o processador (CPU) e os ingredientes do bolo são os dados de entrada. O processo é a atividade consistindo na leitura da receita, busca de ingredientes e preparo do bolo por nosso cientista. 

Agora imagine que o filho do cientista de computação aparece correndo chorando, dizendo que foi picado por uma abelha. O cientista de computação registra onde ele estava na receita (o estado do processo atual é salvo), pega um livro de primeiros socorros e começa a seguir as orientações. Aqui vemos o processador sendo trocado de um processo (preparo do bolo) para um processo mais prioritário (prestar cuidado médico), cada um tendo um programa diferente (receita versus livro de primeiros socorros). Quando a picada de abelha tiver sido cuidada, o cientista de computação volta para o seu bolo, continuando do ponto onde ele havia parado. 

A ideia fundamental aqui é que um processo é uma atividade de algum tipo. Ela tem um programa, uma entrada, uma saída e um estado. Um único processador pode ser compartilhado entre vários processos, com algum algoritmo de escalonamento sendo usado para determinar quando parar o trabalho em um processo e servir outro. Em comparação, um programa é algo que pode ser armazenado em disco sem fazer nada.

**OBS:** Vale a pena observar que se um programa está sendo executado duas vezes, é contado como dois processos. O sistema operacional pode ser capaz de compartilhar o código entre eles de maneira que apenas uma cópia esteja na memória, mas isso é um detalhe técnico que não muda a situação conceitual de dois processos sendo executados!

## Fatores de criação de um processo

1. Inicialização do sistema.
2. Execução de uma chamada de sistema de criação de processo por um processo em execução. 
3. Solicitação de um usuário para criar um novo processo. 
4. Início de uma tarefa em lote.

**OBS:** Processos que ficam em segundo plano são chamados de **daemons**. Tanto no sistema UNIX quanto no Windows, após um processo ser criado, o pai e o filho têm os seus próprios espaços de endereços distintos. Se um dos dois processos muda uma palavra no seu espaço de endereço, a mudança não é visível para o outro processo. Quando o processo filho compartilha a memória com o processo pai usando o sistema _copy-on-write_ (cópia-na-escrita), ambos acessam a mesma memória inicialmente. No entanto, ao tentar modificar algum dado, uma cópia desse trecho é feita para garantir que a alteração ocorra em uma área privada. Assim, nenhuma memória modificável é realmente compartilhada. O filho pode, no entanto, compartilhar outros recursos do pai, como arquivos abertos. No Windows, os espaços de memória do pai e do filho são separados desde o início.

## Fatores de encerramento de um processo

1. Saída normal (voluntária). 
2. Erro fatal (involuntário). 
3. Saída por erro (voluntária). 
4. Morto por outro processo (involuntário).

## Estados de um processo

1. Em execução (realmente usando a CPU naquele instante). 
2. Pronto (executável, temporariamente parado para deixar outro processo ser executado). 
3. Bloqueado (incapaz de ser executado até que algum evento externo aconteça).

	![[Pasted image 20241103072330.png]]

OBS.: O escalonador é o mais baixo nível de um SO estruturado em processos. Logo acima, estão os processos em si
	![[Pasted image 20241103074254.png]]


## Implementação de um processo

Abaixo, há uma tabela de processo (Process Control Block - PCB), que contém informações fundamentais para gerir um processo:

![[Pasted image 20241103074944.png]]

Associada com cada classe de E/S há um local (geralmente em um local fixo próximo da parte inferior da memória) chamado de vetor de interrupção:
### Passo a Passo de Tratamento de Interrupção (com divisão entre Hardware e Sistema Operacional)

1. **Detecção da Interrupção** _(Feito pelo Hardware - CPU)_:
    
    - Quando um dispositivo (por exemplo, de E/S) ou outro componente sinaliza uma interrupção, a CPU detecta esse sinal e interrompe a execução do processo atual automaticamente.
    - A CPU identifica o tipo de interrupção e prepara-se para redirecionar a execução para o vetor de interrupção correspondente.
2. **Salvamento Automático do Estado Inicial** _(Feito pelo Hardware - CPU)_:
    
    - A CPU salva automaticamente algumas informações críticas do estado do processo atual, incluindo:
        - **Contador de programa (PC)**: endereço da próxima instrução do processo interrompido.
        - **Palavra de estado do programa (PSW)** e, em alguns casos, um ou mais **registradores**.
    - Esse salvamento inicial permite que o processo interrompido possa ser retomado exatamente do ponto onde parou após a interrupção ser tratada.
3. **Desvio para o Vetor de Interrupção** _(Feito pelo Hardware - CPU)_:
    
    - A CPU redireciona a execução para o endereço do **vetor de interrupção**. Esse endereço aponta para a rotina que vai tratar o tipo específico de interrupção.
    - O desvio ocorre automaticamente, com base nas informações de hardware definidas para tratar cada tipo de interrupção.
4. **Execução da Rotina de Interrupção Inicial em Assembly** _(Feito pelo Sistema Operacional - Software)_:
    
    - Agora o **sistema operacional** assume o controle. Ele começa executando uma **rotina de serviço de interrupção** em assembly para salvar os registradores restantes e preparar o ambiente de execução para o tratamento.
    - Nesse momento:
        - Os registradores do processo interrompido são salvos (geralmente na **tabela de processo - PCB** do processo).
        - O ponteiro de pilha é limpado e ajustado para uma pilha temporária que será usada durante o tratamento.
5. **Chamada para a Rotina de Interrupção em Alto Nível (em C)** _(Feito pelo Sistema Operacional - Software)_:
    
    - Após a configuração inicial, o sistema operacional chama uma **rotina de interrupção em linguagem de alto nível** (geralmente C) para realizar o trabalho específico relacionado à interrupção (como leitura ou escrita de dados de um dispositivo de E/S).
    - Essa rotina manipula o evento de interrupção de acordo com o que é necessário, acessando e atualizando estruturas de dados do sistema, se necessário.
6. **Escalonador Decide o Próximo Processo a Executar** _(Feito pelo Sistema Operacional - Software)_:
    
    - Quando o tratamento da interrupção termina, o sistema operacional chama o **escalonador** para decidir qual processo deve ser executado a seguir.
    - O escalonador consulta a lista de processos, verifica seus estados e prioridades, e escolhe o próximo processo que será colocado em execução.
7. **Restauração do Estado do Próximo Processo** _(Feito pelo Sistema Operacional - Software)_:
    
    - O sistema operacional usa as informações salvas na **tabela de processo (PCB)** do próximo processo para restaurar seu estado, incluindo os valores dos registradores e o ponteiro de pilha.
    - Isso garante que o próximo processo retome sua execução com o estado que tinha antes de ser interrompido.
8. **Retorno ao Processo ou Início do Próximo** _(Feito pelo Hardware - CPU e Sistema Operacional - Software)_:
    
    - A execução retorna ao processo em execução (ou ao próximo processo, caso uma troca de contexto seja necessária).
    - A CPU retoma a execução a partir do ponto em que o processo parou, usando o **contador de programa** (PC) restaurado e os registradores carregados.


	![[Pasted image 20241103083040.png]]


## Modelando a Multiprogramação

- O uso da CPU pode ser analisado sob uma perspectiva probabilística.
- Considere que um processo passa uma fração **p** do seu tempo esperando a conclusão de dispositivos de E/S.
- Com **n** processos na memória, a probabilidade de que todos os processos estejam esperando por E/S (resultando em CPU ociosa) é **p^n**.
- A fórmula para a utilização da CPU é:

  **Utilização da CPU = 1 – p^n**

### Análise da Utilização da CPU

#### Modelo Probabilístico

O modelo que analisamos anteriormente sobre a utilização da CPU é uma **aproximação**. Ele assume que todos os **n** processos que estão na memória são **independentes** uns dos outros. Por exemplo, em um sistema com cinco processos, é possível que três estejam em execução ao mesmo tempo, enquanto dois estão esperando por operações de E/S (entrada/saída).

#### Limitações do Modelo

No entanto, com apenas uma CPU, não é possível executar três processos simultaneamente. Quando a CPU está ocupada, qualquer outro processo que se torne "pronto" para execução deve esperar até que a CPU fique livre. Isso significa que os processos não são realmente independentes, como o modelo sugere. Um modelo mais preciso poderia ser desenvolvido usando a **teoria das filas**, que leva em conta essa dependência entre os processos.

#### Validade do Ponto Principal

Apesar das limitações, a ideia principal ainda é válida: a multiprogramação permite que os processos usem a CPU mesmo quando ela estaria ociosa em outras circunstâncias. Isso significa que a multiprogramação melhora a utilização da CPU, mesmo que as proporções exatas de utilização possam diferir.

#### Exemplo de Utilização da CPU

Considere um computador com **8 GB** de memória total:

- **2 GB** são usados pelo sistema operacional e suas tabelas.
- Cada programa de usuário ocupa **2 GB**.

Isso permite que **três programas de usuários** estejam na memória ao mesmo tempo. Se a média de espera por E/S for **80%**, a utilização da CPU seria calculada como:  
**Utilização da CPU = 1 – 0,83 = 49%** (onde 0,83 representa a fração de tempo em que os processos estão esperando por E/S).

#### Impacto da Adição de Memória

Se adicionarmos **mais 8 GB** de memória, o número de programas que podem estar na memória simultaneamente aumenta de três para **sete**, elevando a utilização da CPU para **79%**. Isso representa um aumento de **30%** na utilização da CPU. Se adicionarmos mais **8 GB** (totalizando **24 GB**), a utilização da CPU aumentaria apenas de **79% para 91%**, resultando em um aumento de apenas **12%**.