O melhoramento na performance pode ser feito de duas formas: reduzindo a taxa de miss ou reduzindo a punição por miss. Primeiramente, vamos discutir a performance em si e como ela pode ser medida.
Aqui, apenas adicionamos os ciclos os quais são desperdiçados enquanto buscamos informações na memória:

$$CPUTime = (CPUExec + MemoryStallClockCycle)*clockCycleTime$$
$$MemoryStallClockCycle = (ReadStallCycle) + (WriteStallCycle) $$

Os readStallCycle podem ser definidos em termos do número de acessos de leitura por programa, da penalidade de falta em ciclos de clock para uma leitura e da taxa de falta de leitura:

$$\text{readStallCycle} = \frac{\text{reads} }{\text{program}} \times \text{readMissRate} \times \text{readMissPenalty}$$
Em relação à leitura...

Leituras são mais complicadas. Para um esquema write-through, temos duas fontes de stall: write misses, que geralmente necessitam que façamos um fetch do bloco antes de continuar a escrita e o write buffer stalls, que ocorre quando o write buffer está cheio durante a escrita. Por fim, os ciclos parados por operação de escrita são descritos por:


$$\text{writeStallCycle} = \frac{\text{writes} }{\text{program}} \times \text{writeMissRate} \times \text{writeMissPenalty} + \text{writeBufferStalls}$$

Na maioria das organizações de cache de escrita direta, as penalidades por leitura e escrita são as mesmas (o tempo para buscar o bloco na memória). Se assumirmos que as interrupções do buffer de escrita são negligenciáveis, podemos combinar as leituras e escritas usando uma única taxa de falta e a penalidade por falta:

$$\text{MemoryStallClockCycle} = \frac{\text{MemoryAcesss} }{\text{program}} \times \text{MissRate} \times \text{MissPenalty}$$

Ou
$$\text{MemoryStallClockCycle} = \frac{\text{Instructions} }{\text{program}} \times \frac{\text{Misses}}{\text{Instructions}} \times \text{MissPenalty}$$

##### Exemplo: Assume the miss rate of an instruction cache is 2% and the miss rate of the data cache is 4%. If a processor has a CPI of 2 without any memory stalls and the miss penalty is 100 cycles for all misses, determine how much faster a processor would run with a perfect cache that never missed. Assume the frequency of all loads and stores is 36%.


Em termos do contador de instruções $I$
$$Instruction miss cycles = I \times 0,02 \times 100 = 2I$$

Como a frequência de todas os loads e stores são de 36%, podemos encontrar o número de ciclos perdidos de memória para referências de dados
$$\text{Data miss cycle} = I \times 0,36 \times 0,04 \times 100 = 1,44I$$

O número total de memory stalls é $$\text{Memory stalls = 2I + 1,44I = 3,44I}$$
Há mais de três ciclos de espera de memória por instrução. Consequentemente, o CPI total, incluindo as esperas de memória, é de 2 + (3.44 * 1) = 5,44. Como não há alteração na contagem de instruções ou na taxa de clock, a razão dos tempos de execução da CPU é 5,44/2 = 2,72.



#### 1 - reducing the miss by reducing the probability that two different memory blocks will contend for the same cache location

A ideia é não mapear diretamente, ou seja, onde tiver espaço, dispor o bloco. O esquema é chamado de *fully associative*. Para achar um lugar vazio, precisa-se fazer uma pesquisa, que é feita em paralelo a um comparador associado com cada entrada de cache (aumenta o custo de hardware).

O meio termo entre fully e direct é o Set associative, que determina uma quantidade *n* de locais a serem associados (n-way).

![[Pasted image 20231109102308.png]] 
Exemplo de direct (1-way), 2-way e fully associative

![[Pasted image 20231109102559.png]]



Na one-way (mapeamento direto) a taxa de miss é maior, porém a latência é menor - muito utilizada em L1, enquanto na full-way a latência é maior, mas a taxa de miss é menor - empregada no último level da cache.

#### Exemplo:  Assume there are three small caches, each consisting of four one-word blocks. One cache is fully associative, a second is two-way set-associative, and the third is direct-mapped. Find the number of misses for each cache organization given the following sequence of block addresses: 0, 8, 0, 6, and 8. *


##### One-way:

Primeiro, vamos determinar para qual bloco de cache cada endereço de bloco é mapeado:

|   |   |
|---|---|
|Block address|Cache block|
|0|0 mod 4 = 0|
|8|8 mod 4 = 0|
|6|6 mod 4 = 2|

Mapeando…

![[Pasted image 20231113094811.png]]

Total de 5 misses

##### Two-way set-associative:

Nesse caso, teremos 2 sets com índice 0 e 1, com 2 elementos por set

|   |   |
|---|---|
|Block address|Cache set|
|0|0 mod 2 = 0|
|8|8 mod 2 = 0|
|6|6 mod 2 = 0|

  

Como podemos escolher qual entrada em um conjunto substituir em caso de erro, precisamos de uma regra de substituição. Caches associativos de conjunto geralmente substituem o bloco menos usado recentemente dentro de um conjunto; isto é, o bloco que foi mais utilizado no passado é substituído. Usando essa regra:


![[Pasted image 20231113094829.png]]  

Total de 4 misses


#### Fully associative

O cache totalmente associativo possui quatro blocos de cache (em um único conjunto); qualquer bloco de memória pode ser armazenado em qualquer bloco de cache, sem índices. Não precisamos nem saber para qual bloco ou set ele será mapeado, pois não tem mapping:

![[Pasted image 20231113095919.png]]

O cache totalmente associativo tem o melhor desempenho, com apenas três erros

#### 2 -Reducing the Miss Penalty Using Multilevel Caches

A ideia é basicamente colocar mais níveis de cache (geralmente até 3) para que haja mais conteúdo da cache, evitando possíveis misses. Obviamente, a latência é maior ao se buscar na cache level 3, mas diminui a chance de ter de ir na memória RAM (inferno). O problema é que, ao adicionar mais levels de cache, estamos apostando que haverá muitos poucos misses, pois se houve, será o pior caso possível - estamos falando de uma latência absurda.

##### Exemplo: Suppose we have a processor with a base CPI of 1.0, assuming all references hit in the primary cache, and a clock rate of 4 GHz. Assume a main memory access time of 100 ns, including all the miss handling. Suppose the miss rate per instruction at the primary cache is 2%. How much faster will the processor be if we add a secondary cache that has a 5 ns access time for either a hit or a miss and is large enough to reduce the miss rate to main memory to 0.5%?

Se ele realiza  $4.10^9$  clocks por segundo , e o tempo de acesso é de $100 \, ns$, então

$$\frac{100\,ns} {\frac{0,25ns}{clockCycle}} = 400 \, clock cycles$$
O CPI efetivo é dado por

$$CPI = Base CPI + MemoryStallCyclesPerInstructions$$
$$CPI = 1 + 0,02 \times 400 = 9$$

Com 2 levels de cache, um miss no primeiro level pode ser satisfeito também por uma cache secundária ou pela memória principal. A taxa de penalidade por um acesso no segundo nível é:
$$\frac{5\,ns} {\frac{0,25ns}{clockCycle}} = 20 \, clock cycles$$
Se a falta for atendida na cache secundária, então esta é a penalidade total por falta. Se a falta precisar acessar a memória principal, então a penalidade total por falta é a soma do tempo de acesso à cache secundária e do tempo de acesso à memória principal. Assim, para uma cache de dois níveis, o CPI total é a soma dos ciclos de espera de ambos os níveis de cache e do CPI base:

$$CPI = \text{Primary stalls per instructions} + \text{Secundary stalls per instructions} = 1 + (0,02 \times20) + (0,005 \times 400) = 3,4 $$

Então o processador com a cache secundária inserida será mais rápido em $9/3,4 = 2,6$

#### 3 - Software Optimization via Blocking

Nesse caso, devemos sempre explorar o princípio da localidade. Tomemos como exemplo uma matriz quadrada 5x5:

|   |   |   |   |   |
|---|---|---|---|---|
|0|1|2|3|4|
|5|6|7|8|9|
|10|11|12|13|14|
|15|16|17|18|19|
|20|21|22|23|24|

Vamos supor duas situações, a primeira o loop percorrendo por colunas e a outra por linhas. Sabemos que o computador não ver dimensões, portanto ele veria tudo da seguinte forma: 0 1 2 3 4 5 6 7 8 9 10 ... 24. Dessa forma, uma iteração linha a linha, ficaria assim: 0 5 10 15 20. Enquanto uma coluna por coluna: 0 1 2 3 4 5 6. Percebe-se facilmente que a iteração por coluna explora o princípio da localidade. Mas como? O computador aloca blocos de tamanhos variados, então quando ele acessa o 1, ele possivelmente acessa o 4 também, ou seja, ela trás o bloco inteiro consigo. Quando pegamos valores distantes na memória, desperdiçamos o outros que vieram junto no bloco e, pior, temos de fazer o fetch em outro bloco que contém aquele número. Ineficiente.


#### Métodos que exploram as localidades em java

OBS: possivelmente está errado esse código, pois considerei instruções em alto nível, mas devem ser de baixo nível (assembly)

```java
// Demonstração de alta localidade de dados
void muitaLocalidadeDados() {
    int largura = 100000;
    int arr[] = new int[largura];
    for (int i = 0; i < largura - 1; i++) {
        arr[i] = i; // Preenche o array com valores sequenciais
    }
}

// Demonstração de baixa localidade de dados
void poucaLocalidadeDados() {
    Random rd = new Random(10000);
    int arr[] = new int[10000];
    for (int i = 0; i < arr.length; i++) {
        arr[i] = rd.nextInt(i); // Preenche o array com valores aleatórios
    }
}

// Demonstração de alta localidade de instruções
void muitaLocalidadeInstrucoes() {
    int valor = 0;
    for (int i = 0; i < 100000; i++) {
        valor += 1; // Executa a mesma instrução repetidamente
    }
}

// Demonstração de baixa localidade de instruções
void poucaLocalidadeInstrucoes() {
    int valor = 0;
    for (int i = 0; i < 1000; i++) {
        if (i % 2 == 0) {
            valor += i; // Executa diferentes instruções em cada iteração
        } else {
            valor -= i;
        }
    }
}

```
