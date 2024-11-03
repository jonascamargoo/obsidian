## O que é uma thread?

Uma **Thread é a menor unidade de processamento que pode ser gerenciada por um sistema operacional**. Ela representa uma sequência de instruções programadas que pode ser executada de forma independente em um núcleo de CPU. Dentro do mesmo processo, múltiplas threads podem ser utilizadas para realizar tarefas de forma **concorrente**, visando melhorar a eficiência do programa, enquanto uma thread aguarda por uma ação demorada, como uma requisição HTTP, o programa pode prosseguir com a execução de outras threads. As threads de um mesmo programa compartilham o mesmo espaço de memória e os recursos alocados. Sistemas que possuem múltiplas CPUs, ou CPUs com múltiplos núcleos, podem executar threads simultaneamente em núcleos diferentes da CPU, permitindo o **paralelismo**. Imagine as threads como várias tarefas menores que precisam ser realizadas em um churrasco.

### Diferença entre processo e thread

Processos são usados para agrupar recursos, threads são as entidades escalonadas para execução na CPU. O que os threads acrescentam para o modelo de processo é permitir que ocorram múltiplas execuções no mesmo ambiente, com um alto grau de independência uma da outra. Ter múltiplos threads executando em paralelo em um processo equivale a ter múltiplos processos executando em paralelo em um computador. No primeiro caso, os threads compartilham um espaço de endereçamento e outros recursos. No segundo caso, os processos compartilham memórias físicas, discos, impressoras e outros recursos. Como threads têm algumas das propriedades dos processos, às vezes eles são chamados de *processos leves*.

## O que é Multithreading?

**Multithreading** é uma técnica de programação que consiste na criação de múltiplas threads (fluxos de execução independentes) dentro de um único processo. Cada thread pode ser responsável por diferentes tarefas ou partes de uma tarefa mais ampla. Este método pode ser aplicado **tanto em contextos concorrentes quanto paralelos**. Em sistemas com **um único núcleo do processador, o multithreading facilita a concorrência** (alternância rápida entre threads para criar a ilusão de simultaneidade). Já em sistemas **multiprocessadores, ou com múltiplos núcleos**, o multithreading pode alcançar paralelismo real, com threads sendo executadas simultaneamente em núcleos distintos da CPU**, otimizando o uso dos recursos e melhorando a eficiência e o desempenho do processo.

Para ilustrar o conceito de multithread, pense em seu **restaurante favorito**. Aqui, o **processo é o restaurante funcionando**, com o objetivo de **servir comida aos clientes**. Durante um horário de pico, como o almoço em um dia útil, as **threads são como os funcionários da cozinha**. Cada cozinheiro (thread) é **responsável por preparar um prato diferente simultaneamente**, acelerando o atendimento dos pedidos. Dessa forma, vários pratos são preparados ao mesmo tempo, aumentando a eficiência e diminuindo o tempo de espera dos clientes.

## Exemplo do uso de threads usando como analogia a escrita de um livro

**Processador de Texto com Threads**: Em um processador de texto, é comum que o usuário trabalhe com um documento grande, como um livro. Manter o texto em um único arquivo facilita buscas e substituições globais, mas pode tornar o processamento lento, especialmente ao reformatar páginas após mudanças.

**Threads para Paralelismo**: Com threads, o programa pode dividir tarefas, como interação com o usuário, reformatar o documento e salvar backups, cada uma em um thread separado. Por exemplo:

- **Thread 1**: Interage com o usuário, respondendo imediatamente a comandos de rolagem e edição.
- **Thread 2**: Reformatar o documento em segundo plano após edições, como uma mudança na página 1 que afeta o layout das páginas seguintes.
- **Thread 3**: Realiza backups automáticos do documento, protegendo contra a perda de dados sem interferir no trabalho principal.

	![[Pasted image 20241103113112.png]]

Com três threads, o modelo de programação é muito mais simples: o primeiro thread apenas interage com o usuário, o segundo reformata o documento quando solicitado, o terceiro escreve os conteúdos da RAM para o disco periodicamente. Se o programa tivesse apenas um thread, então sempre que um backup de disco fosse iniciado, comandos do teclado e do mouse seriam ignorados até que o backup tivesse sido concluído.


## Exemplo do uso de threads com servidores web

**Servidor Web com Threads**: Em um servidor de website, as solicitações de páginas são enviadas pelos clientes e processadas para retornar rapidamente o conteúdo. Como algumas páginas são solicitadas com mais frequência, o servidor usa um **cache** para armazená-las em memória, evitando o acesso constante ao disco.

**Organização do Servidor com Threads**:

- **Thread Despachante**: Recebe as solicitações e distribui o trabalho aos threads "operários" ociosos.
- **Threads Operários**: Cada thread operário recebe uma solicitação, verifica o cache e responde ao cliente. Se a página solicitada está no cache, o operário a retorna imediatamente. Se não está, ele a carrega do disco.

**Funcionamento**:

- O despachante, em um laço contínuo, atribui as solicitações aos threads operários disponíveis.
- Cada operário, também em um laço, lida com uma solicitação de cada vez, consultando o cache e, se necessário, buscando a página do disco.
- Se um thread operário é bloqueado (por exemplo, durante o acesso ao disco), o sistema permite que outro thread continue a execução, garantindo que o servidor permaneça ativo e eficiente.

``` C
# Thread despachante
while(TRUE) {
	get_next_request(&buf);
	handoff_work(&buf);
}

# Thread operária
while(TRUE) {
	wait_for_work(&buf)
	look_for_page_in_cache(&buf, &page);
	if (page_not_in_cache(&page))
		read_page_from_disk(&buf, &page);
	return_page(&page);
}
```

### O mesmo caso, porém sem thread

Esse exemplo ilustra as limitações de um servidor web sem threads e os benefícios que o uso de threads traz ao desempenho.

**Servidor Web Sem Threads**: Em um modelo de thread único, o servidor processa cada solicitação de maneira sequencial. Ele:

1. Recebe uma solicitação.
2. Processa-a até o fim (incluindo o acesso ao disco, se necessário).
3. Somente após concluir a solicitação, ele passa a processar a próxima.

**Problemas**:

- **Ociosidade da CPU**: Quando o servidor aguarda uma resposta do disco, a CPU permanece ociosa, já que não há outro trabalho sendo realizado em paralelo.
- **Baixo Desempenho**: Com a CPU inativa durante a espera, o servidor processa muito menos solicitações por segundo, reduzindo sua capacidade de atendimento.

**Benefício dos Threads**: Com threads, o servidor pode lidar com várias solicitações simultaneamente. Enquanto um thread espera pelo disco, outros threads podem processar novas solicitações, aproveitando a CPU o máximo possível. Isso aumenta o número de solicitações processadas por segundo e melhora o desempenho geral sem complicar a programação, pois cada thread ainda opera de forma sequencial.

### Servidor Web com E/S Sem Bloqueio: Simulando Concorrência com Máquina de Estados Finitos


Esse terceiro exemplo descreve uma abordagem alternativa para implementar um servidor web quando threads não estão disponíveis e o desempenho de um único thread é insatisfatório. A solução usa operações de E/S de disco sem bloqueio para simular o processamento concorrente.

**Servidor Web com E/S Sem Bloqueio**:

- Quando uma solicitação é recebida, o servidor examina se ela pode ser atendida pelo cache. Se sim, responde imediatamente.
- Se a página não está no cache, o servidor inicia uma operação de leitura de disco **sem bloqueio** e registra o estado da solicitação em uma tabela, permitindo que o servidor prossiga com outras solicitações.

**Eventos e Controle de Estado**:

- Como o servidor continua processando novos pedidos enquanto espera a resposta do disco, ele trabalha com eventos:
    - Um evento pode ser uma nova solicitação, que o servidor começa a processar.
    - Ou pode ser uma resposta do disco referente a uma solicitação anterior, que ele recupera da tabela para dar continuidade.
- Esse sistema exige que o servidor salve e restaure o estado de cada solicitação, registrando detalhes como o progresso da leitura e a posição na tabela de estados.

**Modelo de Máquina de Estados Finitos**:

- Nesse design, o servidor age como uma **máquina de estados finitos**. Cada solicitação passa por estados específicos (por exemplo, “esperando por E/S”, “processando resposta do disco”) e o servidor troca entre esses estados conforme recebe eventos.
- Embora essa abordagem seja eficiente, ela exige mais complexidade no gerenciamento dos estados e simula, de certa forma, a execução concorrente sem a simplicidade de threads.

Resumo dos 3

![[Pasted image 20241103123249.png]]
