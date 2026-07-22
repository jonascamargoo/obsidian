---
tipo: conceito
area: Sistemas Operacionais
tags:
- so
criada: '2025-01-10'
---

## Categorias de Algoritmos de Escalonamento
Existem diferentes algoritmos de escalonamento dependendo do ambiente e das metas específicas de cada tipo de sistema operacional. Três ambientes principais são:
### Lote
Sistemas usados em tarefas como processamento de folha de pagamento, estoque e cálculos bancários. Algoritmos não preemptivos ou preemptivos com longos períodos de execução são comuns, pois o tempo de resposta rápido não é necessário.
### Interativo
Sistemas que servem a múltiplos usuários, onde a preempção é crucial para garantir que um processo não ocupe a CPU indefinidamente, prejudicando a experiência de outros usuários.
### Tempo Real
Sistemas com requisitos rigorosos de tempo, onde, em alguns casos, a preempção não é necessária. Processos em tempo real devem cumprir prazos rigorosos para evitar falhas no sistema.
### Objetivos do Algoritmo de Escalonamento
Os objetivos de um algoritmo de escalonamento variam conforme o ambiente, mas alguns são aplicáveis a todos os sistemas:

* Garantir que processos comparáveis recebam serviços proporcionais;
* A política de prioridade do sistema deve ser respeitada;
* Manter a CPU e outros dispositivos de E/S ocupados para aumentar a eficiência;
* Maximizar o número de tarefas concluídas por hora;
* Minimizar o tempo entre o envio e a conclusão de uma tarefa (importante em sistemas em lote);
* Reduzir o tempo entre o envio de um comando e a resposta do sistema (importante em sistemas interativos);
* Satisfazer as expectativas do usuário em relação ao tempo de resposta, com base na complexidade da tarefa;
* Garantir que os prazos sejam cumpridos para evitar falhas, especialmente em sistemas de controle de dispositivos ou multimídia;
* Foco em tempo de retorno e utilização da CPU;
* Enfatizam tempo de resposta e proporcionalidade;
* Foco no cumprimento de prazos e previsibilidade, especialmente em sistemas multimídia.

## Escalonamento em sistemas em lote

Chegou o momento de passar das questões gerais de escalonamento para algoritmos específicos. Nesta seção, examinaremos os algoritmos usados em sistemas em lote, e nas seções seguintes abordaremos sistemas interativos e de tempo real. Alguns algoritmos são utilizados tanto em sistemas interativos quanto em sistemas em lote, sendo esses discutidos mais tarde.

### Primeiro a Chegar, Primeiro a Ser Servido

O algoritmo _Primeiro a Chegar, Primeiro a Ser Servido_ (First-Come, First-Served - FCFS) é um dos mais simples algoritmos de escalonamento e não é preemptivo. Neste modelo, a CPU é atribuída aos processos na ordem em que são requisitados. Os processos ficam em uma fila única, e o primeiro que entra no sistema é iniciado imediatamente, sendo executado até ser bloqueado ou concluído. Os processos subsequentes entram na fila e são atendidos sequencialmente.

#### Vantagens

- Simplicidade: É fácil de entender e implementar.
- Justo: Processos são atendidos de acordo com sua chegada, como uma fila de ingressos ou serviços.

#### Desvantagens

- **Problema de processo limitado pela CPU**: Em um cenário onde um processo computacionalmente intensivo é seguido por muitos processos de E/S (entrada/saída), o algoritmo pode ser ineficiente. Por exemplo, um processo limitado pela E/S pode demorar muito para ser concluído, afetando negativamente os tempos de retorno dos outros processos. Se fosse utilizado um algoritmo preemptivo, o processo de E/S terminaria mais rapidamente, sem afetar tanto os outros.

### Tarefa Mais Curta Primeiro

O algoritmo _Tarefa Mais Curta Primeiro_ (Shortest Job First - SJF) assume que os tempos de execução dos processos são conhecidos antecipadamente. O escalonador escolhe o processo com o menor tempo de execução, o que ajuda a reduzir o tempo médio de espera. Esse algoritmo é especialmente útil em cenários como companhias de seguros, onde o tempo de execução pode ser estimado com precisão.

#### Exemplo

Dada uma fila com quatro tarefas de tempos de execução de 8, 4, 4 e 4 minutos, respectivamente, executá-las na ordem correta resulta em uma média de 11 minutos de tempo de retorno, enquanto executá-las em ordem inversa pode resultar em uma média de 14 minutos.

#### Desvantagens

- **Quando as tarefas não estão disponíveis simultaneamente**: O algoritmo não é ótimo quando as tarefas chegam em momentos diferentes. Por exemplo, se as tarefas A, B, C e D possuem tempos de execução de 2, 4, 1, 1 e 1, respectivamente, mas chegam em momentos diferentes, o tempo de espera médio pode ser maior do que o esperado.

### Tempo Restante Mais Curto em Seguida

A versão preemptiva do _Tarefa Mais Curta Primeiro_ é chamada _Tempo Restante Mais Curto em Seguida_ (Shortest Remaining Time Next - SRTN). Nesse algoritmo, o escalonador escolhe o processo cujo tempo restante de execução é o mais curto. Se uma nova tarefa chega com tempo de execução menor do que o tempo restante do processo atual, este é interrompido, e a nova tarefa é iniciada.

#### Vantagens

- **Desempenho para tarefas curtas**: Esse algoritmo favorece tarefas curtas, permitindo que elas sejam concluídas mais rapidamente, o que melhora o desempenho do sistema.

#### Desvantagens

- **Necessidade de conhecimento prévio**: O tempo de execução dos processos precisa ser conhecido antecipadamente, o que pode não ser viável em sistemas dinâmicos.


## Escalonamento em sistemas interativos

**Escalonamento por chaveamento circular**

- O algoritmo circular (round-robin) é simples, justo e amplamente utilizado. Cada processo recebe um quantum de tempo. Quando o quantum se esgota, o processo é preemptado e o próximo na fila é executado.
- O comprimento do quantum é importante: um quantum muito curto pode levar a muitos chaveamentos, prejudicando a eficiência da CPU, enquanto um quantum muito longo pode resultar em respostas ruins para tarefas curtas.
- Normalmente, um quantum entre 20-50 ms é adequado.

**Escalonamento por prioridades**

- Processos podem ser escalonados com base em suas prioridades. Processos com maior prioridade são executados primeiro.
- As prioridades podem ser estáticas (predefinidas) ou dinâmicas (ajustadas conforme a execução do processo).
- Sistemas de escalonamento podem ter múltiplas filas de prioridade, onde processos de prioridade mais alta são executados antes, com escalonamento circular dentro de cada classe de prioridade.
- Pode haver um ajuste de prioridade para evitar que processos de maior prioridade monopolizem a CPU.

**Múltiplas filas**

- Para melhorar a eficiência, os sistemas podem usar múltiplas filas de prioridade, com cada classe de prioridade recebendo diferentes quantidades de quantum. Isso evita que processos de longa duração causem muitos chaveamentos, enquanto ainda prioriza tarefas interativas curtas.

**Processo mais curto em seguida (Shortest Job Next)**

- A ideia é executar primeiro os processos com menor tempo de execução. Isso pode ser benéfico para sistemas interativos, onde os processos tendem a seguir um padrão de alternância entre espera e execução.
- Pode-se usar uma estimativa do tempo de execução de um processo com base no seu histórico de execução.

**Escalonamento garantido**

- O sistema pode fazer promessas de distribuição justa de CPU entre os usuários. Cada usuário tem direito a uma fração da CPU, e o escalonamento garante que isso seja cumprido.

**Escalonamento por loteria**

- Nesse modelo, cada processo recebe "bilhetes de loteria", e um bilhete é sorteado aleatoriamente para determinar qual processo executará. A quantidade de bilhetes pode ser ajustada para refletir a importância de um processo.

**Escalonamento por fração justa**

- A alocação de CPU é ajustada para garantir que os usuários recebam a CPU de maneira proporcional ao seu número de processos. Isso evita que um usuário com muitos processos monopolize a CPU.

Esses algoritmos têm diferentes características que os tornam mais ou menos adequados para diferentes tipos de sistemas interativos. O objetivo comum é balancear justiça, eficiência e tempo de resposta, adaptando-se à carga de trabalho do sistema.

## Escalonamento em sistemas de tempo real

Sistemas de tempo real têm um papel essencial do tempo. Em tais sistemas, dispositivos externos ao computador geram estímulos, e o computador deve reagir dentro de um tempo fixo. Exemplos incluem CD players, monitoramento de pacientes, piloto automático de aviões e controle de robôs. A resposta precisa ser no momento certo, caso contrário, pode ser tão ruim quanto uma resposta errada.

Esses sistemas são divididos em **tempo real crítico** (onde há prazos absolutos) e **tempo real não crítico** (onde perder um prazo é indesejável, mas tolerável). Para atender a esses prazos, o programa é dividido em processos previsíveis e rápidos, geralmente com vida útil curta.

Existem eventos **periódicos** (que ocorrem em intervalos regulares) e **aperiódicos** (imprevisíveis). Para que o sistema funcione, a carga total dos eventos periódicos deve ser compatível com a capacidade da CPU, ou seja, a soma do tempo de CPU necessário dividido pelo período de cada evento deve ser menor que 1. Caso contrário, o sistema não é escalonável.

**Exemplo:** Um sistema com três eventos periódicos com períodos de 100, 200 e 500 ms, exigindo 50, 30 e 100 ms de CPU, é escalonável, pois a soma (0,5 + 0,15 + 0,2) é menor que 1. A adição de um quarto evento (1 segundo de período) só é viável se ele não demandar mais que 150 ms de CPU.

Os **algoritmos de escalonamento** podem ser **estáticos** (decisões tomadas antes da execução) ou **dinâmicos** (decisões tomadas durante a execução). O escalonamento estático funciona bem com informações perfeitas antecipadas, enquanto o dinâmico não tem essas restrições.

**Política versus Mecanismo**: Um processo com filhos pode querer influenciar o escalonamento. Contudo, os escalonadores comuns não aceitam tais entradas. A solução é separar o **mecanismo** de escalonamento da **política**. O mecanismo fica no núcleo, mas o processo pode controlar a política, como no caso de um algoritmo de prioridades com chamada de sistema para ajustar prioridades de filhos.

## Escalonamento de Threads

Quando múltiplos threads são usados dentro de vários processos, temos dois níveis de paralelismo: **processos** e **threads**. O escalonamento desses sistemas depende se os threads são de **usuário** ou de **núcleo** (ou ambos).

### Threads de Usuário:

- O núcleo não tem conhecimento dos threads, e o escalonador de processos escolhe um processo para executar. Dentro do processo, o escalonador de threads decide qual thread executar.
- Os threads cooperam, ou seja, um thread pode ceder a CPU para outro dentro do processo, sem interrupções do relógio.
- O escalonamento pode ser circular ou por prioridade. Embora os threads não possam ser interrompidos, o sistema normalmente não tem problemas com isso porque os threads cooperam entre si.
- Exemplo: Se um processo tem múltiplos threads com pouco trabalho para fazer, o escalonador pode alternar entre eles rapidamente, como A1, A2, A3, A1, A2, A3, até que o núcleo mude para outro processo.

### Threads de Núcleo:

- O núcleo escolhe um thread para executar, sem se preocupar com a qual processo ele pertence (embora possa considerar isso se necessário).
- O thread recebe um quantum de tempo e, se não terminar, é suspenso. O escalonamento é mais flexível e eficiente, permitindo uma execução mais controlada dos threads.
- O chaveamento de threads de núcleo é mais caro, pois exige troca completa de contexto, mudanças no mapa de memória e invalidação de cache.
- No entanto, quando um thread de núcleo é bloqueado (por exemplo, durante E/S), apenas esse thread é suspenso, e não o processo inteiro.

### Diferenças Importantes:

- **Desempenho:** O chaveamento de threads de usuário é mais rápido do que o de núcleo, devido ao custo de trocar o contexto completo em threads de núcleo.
- **Escalonador de Thread Específico de Aplicação:** Com threads de usuário, é possível usar um escalonador de threads específico para a aplicação, o que permite otimizar o desempenho em cenários como servidores web, onde threads frequentemente ficam bloqueadas por E/S.
- **Eficiência:** Threads de núcleo não têm o conhecimento da aplicação, então o escalonador de núcleo pode não tomar as melhores decisões, enquanto escalonadores específicos de aplicação podem ajustar melhor a execução, melhorando a eficiência.