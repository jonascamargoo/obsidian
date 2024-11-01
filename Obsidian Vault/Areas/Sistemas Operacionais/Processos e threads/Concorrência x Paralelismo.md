
## O que é Concorrência?

**Concorrência é sobre lidar com muitas tarefas ao mesmo tempo**, mas não de forma simultânea. É a habilidade de uma aplicação gerenciar múltiplas tarefas e instruções em segundo plano, mesmo que essas instruções não estejam sendo processadas ao mesmo tempo, ou executadas em outros núcleos do processador.


Imagine que você está preparando um churrasco sozinho. Você é responsável por organizar a geladeira, fazer os cortes de carne, preparar os vegetais para os amigos vegetarianos, fazer caipirinhas e gelar a cerveja. Você alterna entre essas tarefas, trabalhando um pouco em cada uma, apesar de ser responsável por todas elas.

Este cenário é um exemplo de concorrência, onde você está gerenciando várias tarefas, mas não necessariamente trabalhando em mais de uma delas simultaneamente. Você se alterna entre as tarefas, criando a impressão de que tudo está progredindo ao mesmo tempo.

#### Exemplo de implementação

``` Java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.CountDownLatch;
import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.TimeUnit;

class Atividade {
    String nome;
    int tempo;

    public Atividade(String nome, int tempo) {
        this.nome = nome;
        this.tempo = tempo;
    }
}

public class Churrasco {

    // Função para simular o tempo de preparo de cada atividade do churrasco
    public static void preparar(Atividade tarefa, BlockingQueue<String> churrasco, CountDownLatch latch) {
        try {
            System.out.printf("Preparando %s...\n", tarefa.nome);
            TimeUnit.SECONDS.sleep(tarefa.tempo);
            churrasco.put(tarefa.nome);
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            System.out.println("Preparo interrompido para: " + tarefa.nome);
        } finally {
            latch.countDown();
        }
    }

    public static void main(String[] args) {
        // Fila de atividades que compõem o churrasco
        BlockingQueue<String> churrasco = new LinkedBlockingQueue<>();

        // Lista de Atividades do Churrasco
        List<Atividade> tarefas = Arrays.asList(
                new Atividade("picanha", 5),
                new Atividade("costela", 7),
                new Atividade("linguica", 3),
                new Atividade("salada", 2),
                new Atividade("bebidas", 1),
                new Atividade("churrasqueira", 2),
                new Atividade("queijo", 3)
        );

        // CountDownLatch para aguardar todas as tarefas terminarem
        CountDownLatch latch = new CountDownLatch(tarefas.size());

        // Inicia as tarefas em threads
        for (Atividade tarefa : tarefas) {
            new Thread(() -> preparar(tarefa, churrasco, latch)).start();
        }

        // Thread para exibir as atividades preparadas e aguardar a conclusão
        new Thread(() -> {
            try {
                latch.await(); // Espera que todas as tarefas sejam concluídas
                System.out.println("Churrasco terminou :/");
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                System.out.println("Erro ao aguardar término das tarefas");
            }
        }).start();

        // Exibe as atividades conforme elas ficam prontas
        while (latch.getCount() > 0 || !churrasco.isEmpty()) {
            try {
                String item = churrasco.take();
                System.out.printf("%s foi preparado.\n", item);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                System.out.println("Erro ao exibir itens preparados");
            }
        }
    }
}
/*
Preparando picanha...
Preparando salada...
Preparando bebidas...
Preparando linguica...
Preparando churrasqueira...
Preparando costela...
Preparando queijo...
bebidas foi preparado.
salada foi preparado.
churrasqueira foi preparado.
linguica foi preparado.
queijo foi preparado.
picanha foi preparado.
costela foi preparado.
Churrasco terminou :/
*/

```


## O que é Paralelismo?

Ainda estamos no exemplo do churrasco. Desta vez você tem amigos para ajudar: um corta a carne, outro acende a churrasqueira, outro gela a cerveja e mais um faz a caipirinha. Todas essas tarefas estão ocorrendo em paralelo, com cada pessoa responsável por uma parte do processo.

Isso ilustra o paralelismo. **Múltiplas tarefas** e instruções ocorrendo **simultaneamente**, executadas por **múltiplos núcleos de processadores**.

Diferentemente da concorrência, onde se trata de gerenciar várias tarefas ao mesmo tempo, mas com apenas uma ativa por vez, **o paralelismo envolve fazer várias coisas ao mesmo tempo.**

O paralelismo é empregado em situações onde o desempenho e a eficiência são críticos, e há recursos suficientes, como múltiplos núcleos de CPU, para executar diversas tarefas simultaneamente.

Em ambientes paralelos, processos ou threads frequentemente precisam coordenar suas ações e comunicar-se entre si. Mecanismos de sincronização, como **semáforos**, **mutexes** e **monitores**, são ferramentas essenciais para evitar **race conditions** e garantir a consistência dos dados, embora isso possa acrescentar complexidade à programação e ao debugging de programas que implementam paralelismo.

#### Exemplo de implementação

``` Java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.CountDownLatch;
import java.util.concurrent.Executors;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.LinkedBlockingQueue;
import java.util.concurrent.TimeUnit;

class Atividade {
    String nome;
    int tempo;
    int responsavel;

    public Atividade(String nome, int tempo, int responsavel) {
        this.nome = nome;
        this.tempo = tempo;
        this.responsavel = responsavel;
    }
}

public class Churrasco {

    // Função para simular o tempo de preparo de cada atividade do churrasco
    public static void preparar(List<Atividade> atividades, BlockingQueue<Atividade> churrasco, int amigo, CountDownLatch latch) {
        try {
            for (Atividade atividade : atividades) {
                atividade.responsavel = amigo; // Identifica o responsável pela tarefa
                System.out.printf("Amigo %d começou a preparação de %s...\n", amigo, atividade.nome);
                TimeUnit.SECONDS.sleep(atividade.tempo);
                churrasco.put(atividade);
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
            System.out.printf("Preparo interrompido para amigo %d.\n", amigo);
        } finally {
            latch.countDown();
        }
    }

    public static void main(String[] args) {
        // Canal das atividades que compõe o churrasco
        BlockingQueue<Atividade> churrasco = new LinkedBlockingQueue<>();

        // Recuperando o número de CPU's (amigos) disponíveis para ajudar no churrasco
        int numCPU = Runtime.getRuntime().availableProcessors();
        System.out.printf("Número de CPU's (amigos) para ajudar no churrasco: %d.\n", numCPU);

        // Lista de Atividades do Churrasco - Atividade / Tempo de Execução / Amigo Responsável
        List<Atividade> tarefas = Arrays.asList(
                new Atividade("picanha", 5, 0),
                new Atividade("costela", 7, 0),
                new Atividade("linguica", 3, 0),
                new Atividade("salada", 2, 0),
                new Atividade("gelar cerveja", 1, 0),
                new Atividade("organizar geladeira", 1, 0),
                new Atividade("queijo", 3, 0),
                new Atividade("caipirinha", 2, 0),
                new Atividade("panceta", 4, 0),
                new Atividade("espetinhos", 3, 0),
                new Atividade("abacaxi", 3, 0),
                new Atividade("limpar piscina", 1, 0),
                new Atividade("molhos", 2, 0),
                new Atividade("pão de alho", 4, 0),
                new Atividade("arroz", 4, 0),
                new Atividade("farofa", 4, 0)
        );

        System.out.printf("Número de tarefas do churrasco: %d.\n", tarefas.size());

        // Balanceamento das tarefas entre os amigos (CPUs)
        int sliceSize = (tarefas.size() + numCPU - 1) / numCPU;
        System.out.printf("Número de tarefas para cada CPU (amigo): %d.\n", sliceSize);

        // CountDownLatch para aguardar todas as tarefas terminarem
        CountDownLatch latch = new CountDownLatch(numCPU);

        // ExecutorService para gerenciar threads
        ExecutorService executor = Executors.newFixedThreadPool(numCPU);

        for (int i = 0; i < tarefas.size(); i += sliceSize) {
            int end = Math.min(i + sliceSize, tarefas.size());
            List<Atividade> subTarefas = tarefas.subList(i, end);
            int amigo = i / sliceSize + 1;
            executor.execute(() -> preparar(subTarefas, churrasco, amigo, latch));
        }

        // Thread para exibir as atividades conforme ficam prontas
        new Thread(() -> {
            try {
                latch.await();  // Espera todas as tarefas serem concluídas
                System.out.println("Churrasco terminou :/");
                executor.shutdown();  // Encerra o executor
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                System.out.println("Erro ao aguardar término das tarefas");
            }
        }).start();

        // Exibe as atividades conforme elas ficam prontas
        while (!executor.isTerminated() || !churrasco.isEmpty()) {
            try {
                Atividade atividade = churrasco.take();
                System.out.printf("Amigo %d terminou de preparar %s...\n", atividade.responsavel, atividade.nome);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                System.out.println("Erro ao exibir itens preparados");
            }
        }
    }
}
/*
Número de CPU's (amigos) pra ajudar no churrasco: 8.
Número tarefas do churrasco: 16.
Número tarefas pra cada CPU (amigo): 2.
Amigo 1 começou a prepação de picanha...
Amigo 3 começou a prepação de gelar cerveja...
Amigo 6 começou a prepação de abacaxi...
Amigo 2 começou a prepação de linguica...
Amigo 7 começou a prepação de molhos...
Amigo 5 começou a prepação de panceta...
Amigo 8 começou a prepação de arroz...
Amigo 4 começou a prepação de queijo...
Amigo 3 começou a prepação de organizar geladeira...
Amigo 3 terminou de preparar gelar cerveja...
Amigo 3 terminou de preparar organizar geladeira...
Amigo 7 começou a prepação de pão de alho...
Amigo 7 terminou de preparar molhos...
Amigo 6 começou a prepação de limpar piscina...
Amigo 6 terminou de preparar abacaxi...
Amigo 2 começou a prepação de salada...
Amigo 2 terminou de preparar linguica...
Amigo 4 terminou de preparar queijo...
Amigo 4 começou a prepação de caipirinha...
Amigo 6 terminou de preparar limpar piscina...
Amigo 8 começou a prepação de farofa...
Amigo 8 terminou de preparar arroz...
Amigo 5 terminou de preparar panceta...
Amigo 5 começou a prepação de espetinhos...
Amigo 1 começou a prepação de costela...
Amigo 1 terminou de preparar picanha...
Amigo 2 terminou de preparar salada...
Amigo 4 terminou de preparar caipirinha...
Amigo 7 terminou de preparar pão de alho...
Amigo 5 terminou de preparar espetinhos...
Amigo 8 terminou de preparar farofa...
Amigo 1 terminou de preparar costela...

Program exited.
```


### Paralelismo Interno

O **paralelismo interno**, também conhecido como **paralelismo intrínseco**, ocorre dentro de uma **processo**. É o paralelismo que você **implementa no código da sua aplicação** quando precisa dividir tarefas ou itens em memória entre várias sub-tarefas que podem ser processadas simultaneamente. **Basicamente, é o paralelismo que você cria via código para ser executado dentro do seu container ou servidor**.

### Paralelismo Externo

Já o paralelismo externo refere-se à **execução simultânea de múltiplas tarefas em diferentes hardwares, máquinas ou containers**. Esse conceito é aplicado em ambientes de computação distribuída, como **Hadoop** e **Spark**, consumo de mensagens vindas de message brokers como **RabbitMQ**, **SQS**, streamings como **Kafka** que distribuem grandes volumes de dados em vários servidores e instâncias para realizar tarefas de ETL, Machine Learning e Analytics. Também é visto em **Load Balancers**, que dividem as requisições entre várias instâncias da mesma aplicação para distribuir o tráfego.

## Concorrência vs Paralelismo

A **concorrência** lida com a execução de várias tarefas ao mesmo tempo, permitindo que um sistema execute múltiplas operações aparentemente simultâneas. Já o **paralelismo** envolve a execução literal de várias operações ou tarefas ao mesmo tempo.

Concorrência no mais, significa também ter várias tarefas em paralelo onde você não tem controle na ordem que elas serão processadas, tendo em vista que só é possível saber a ordem de execução após todas elas terem terminado.

Em sistemas com um único núcleo de CPU, a concorrência é normalmente alcançada através de multithreading, onde as tarefas são **alternadas rapidamente**, criando a ilusão de execução simultânea. Por outro lado, o **paralelismo** requer hardware com **múltiplos núcleos**, permitindo que cada núcleo execute **diferentes threads ou processos simultaneamente**.

Paralelismo em geral é concorrente, mas nem toda concorrência é paralela.

![[Pasted image 20241101171131.png]]