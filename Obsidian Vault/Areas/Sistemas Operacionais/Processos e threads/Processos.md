
## O que é um processo?

Um processo é basicamente uma **instância de um programa em execução**. Esse programa contém uma série de instruções, e o processo é a execução real dessas instruções. Em outras palavras, **um processo é um programa em ação**. 

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
