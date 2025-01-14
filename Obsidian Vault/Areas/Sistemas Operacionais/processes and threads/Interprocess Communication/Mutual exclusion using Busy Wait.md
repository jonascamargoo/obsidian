## O que é?

## Soluções utilizando exclusão mútua

### Desabilitação de interrupções:

**Explicação**:  
Nesse método, o processo que deseja acessar a região crítica (onde há memória compartilhada) desabilita todas as interrupções assim que entra nessa área e só as reabilita quando termina. A ideia é que, ao desabilitar as interrupções, o sistema operacional não pode mudar a CPU para outro processo, garantindo que aquele processo terá controle exclusivo da memória compartilhada.

**Problema**:  
Apesar de ser simples, essa técnica tem vários problemas. Primeiro, não é seguro deixar processos de usuário desabilitarem interrupções, pois eles poderiam nunca reativá-las, travando o sistema. Segundo, em sistemas com múltiplos núcleos (multiprocessadores), desabilitar interrupções afeta apenas o núcleo que executa o comando, enquanto os outros continuam funcionando e podem acessar a memória compartilhada, o que torna essa técnica ineficaz em sistemas modernos de múltiplos núcleos.

**Aplicabilidade**:  
Hoje em dia, essa técnica pode ser útil apenas dentro do próprio núcleo do sistema operacional e por um curto período, para garantir que operações críticas, como atualização de listas de processos, não sejam interrompidas.

### Variáveis do tipo trava (lock):

**Explicação**:  
Uma alternativa de software envolve o uso de uma variável compartilhada chamada "trava" ou "lock". Essa variável começa com o valor 0, indicando que nenhum processo está na região crítica. Quando um processo quer entrar, ele verifica o valor da trava. Se for 0, o processo a muda para 1 e entra na região crítica. Se a trava já estiver em 1 (indicando que outro processo está na região crítica), ele espera até que ela volte a 0.

**Problema**:  
Esse método pode falhar em sistemas concorrentes. Imagine que dois processos leem a variável de trava ao mesmo tempo e ambos veem que ela está em 0. Se um deles mudar a trava para 1 enquanto o outro ainda não terminou sua verificação, ambos podem acabar entrando na região crítica ao mesmo tempo, causando o problema que a exclusão mútua deveria evitar.

**Solução inadequada**:  
Mesmo que tentemos melhorar a ideia verificando a trava duas vezes (antes e depois de mudar seu valor), isso não resolve o problema, pois ainda pode haver uma "corrida" entre os processos durante a verificação.


### Alternância explícita (turn-based switching):

**Explicação**:  
Nesse método, dois processos se alternam para entrar na região crítica, controlados por uma variável chamada `turn`. Inicialmente, `turn` é 0, o que significa que o processo 0 pode entrar na região crítica. O processo 1 fica esperando até que `turn` seja 1. Quando o processo 0 sai da região crítica, ele muda `turn` para 1, permitindo que o processo 1 entre na sua vez. Esse método, em essência, faz os dois processos se revezarem.

**Problema**:  
Esse método evita condições de corrida, mas pode levar a ineficiência. Por exemplo, se o processo 1 for mais lento e ficar preso na região não crítica (onde não está manipulando memória compartilhada), o processo 0 não poderá entrar na sua região crítica, mesmo que esteja pronto para isso. Isso desperdiça tempo de CPU, pois o processo 0 fica esperando à toa (espera ocupada), sem que o processo 1 esteja realmente usando a região crítica.

**Desvantagem maior**:  
A alternância forçada viola uma das condições básicas de um bom mecanismo de exclusão mútua: um processo não deve ser bloqueado por outro que não está usando a região crítica. Além disso, como um processo pode ser muito mais rápido que o outro, a alternância rígida acaba se tornando ineficaz em sistemas onde a carga de trabalho dos processos é diferente.


```
// Processo 0
while (TRUE) {
    while (turn != 0) /* laço */;
    critical_region();
    turn = 1;
    noncritical_region();
}

// Processo 1
while (TRUE) {
    while (turn != 1) /* laço */;
    critical_region();
    turn = 0;
    noncritical_region();
}

// dois processos (0 e 1) se revezam para acessar a região crítica com base no valor da variável `turn`
```

### Solução de Peterson

**Explicação**:  
A solução de Peterson foi desenvolvida por G. L. Peterson em 1981 como uma maneira mais simples e eficaz de resolver o problema da exclusão mútua, sem a necessidade de alternância explícita entre processos. Esse algoritmo substituiu a solução anterior de Dekker, que era mais complexa.

**Como a solução de Peterson funciona**:  
**Uso de duas variáveis**: A solução utiliza uma variável chamada `turn` (vez) e um array de variáveis booleanas chamado `interested[]` (interessado). A variável `turn` determina de quem é a vez de entrar na região crítica, enquanto `interested[]` armazena se um processo está interessado em entrar na região crítica.

**Quando um processo deseja entrar na região crítica**:  
O processo chama a função `enter_region()`, indicando seu interesse definindo `interested[process] = TRUE` e ajusta `turn = process`. O processo espera enquanto `turn == process` e `interested[other] == TRUE` (indica que o outro processo também está interessado).

**Quando um processo termina**:  
O processo chama `leave_region()`, que define `interested[process] = FALSE`, indicando que ele não está mais interessado na região crítica.

**Cenário de concorrência**:  
Se ambos os processos chamarem `enter_region()` ao mesmo tempo, o último a atualizar o valor de `turn` cede a vez, garantindo que apenas um processo entre na região crítica de cada vez.

**Vantagens**:  
A solução de Peterson é simples e eficaz para garantir a exclusão mútua entre dois processos, resolvendo o problema de alternância forçada e condições de corrida.

```
#define FALSE 0
#define TRUE 1
#define N 2 /* número de processos */

int turn; /* de quem é a vez? */
int interested[N]; /* todos os valores 0 (FALSE) */

void enter_region(int process) /* processo é 0 ou 1 */
{
    int other; /* número do outro processo */
    other = 1 - process; /* o oposto do processo */
    interested[process] = TRUE; /* mostra que você está interessado */
    turn = process; /* altera o valor de turn */
    
    while (turn == process && interested[other] == TRUE) 
        /* comando nulo */;
}

void leave_region(int process) /* processo: quem está saindo */
{
    interested[process] = FALSE; /* indica a saída da região crítica */
}

// utilizando variáveis de controle `turn` e `interested` para garantir que apenas um processo entre na região crítica de cada vez

```

### Instrução TSL (Test and Set Lock)

**Explicação**:  
A TSL (Test and Set Lock) é uma solução de hardware usada em arquiteturas multiprocessadas. Ao contrário da solução de Peterson, que é puramente software, a TSL depende de uma operação atômica fornecida pelo hardware para garantir a exclusão mútua.

**Como a TSL funciona**:  
**A operação TSL**: A TSL lê o valor de uma variável de trava (`lock`) da memória e a armazena em um registrador. Simultaneamente, define `lock = 1`, indicando que a trava está sendo usada. Isso ocorre de forma atômica, impedindo que outros processos acessem a variável durante a operação.

**Uso para exclusão mútua**:  
O sistema usa a variável `lock` para coordenar o acesso à região crítica. Se `lock == 0`, o processo define `lock = 1` usando a TSL e adquire o direito de acessar a região crítica. Após terminar, define `lock = 0` para liberar a região.

**Bloqueio do barramento de memória**:  
A TSL impede que outras CPUs acessem a memória durante a operação, essencial em sistemas multiprocessados, garantindo que as operações sejam indivisíveis.

**Comparação com desabilitação de interrupções**:  
Diferente de desabilitar interrupções, a TSL depende do hardware, tornando-a mais adequada para sistemas com multiprocessamento.

**Alternativa TSL – Instrução XCHG**:  
O XCHG é outra instrução usada para o mesmo propósito, trocando o valor de um registrador com uma variável de memória de maneira atômica, funcionando de forma semelhante à TSL.

**Vantagens da TSL**:  
A TSL é eficiente em sistemas multiprocessados, garantindo exclusão mútua de forma segura e rápida, utilizando operações atômicas fornecidas pelo hardware.

**Desvantagens**:  
A TSL usa espera ocupada (busy waiting), o que pode desperdiçar recursos de CPU, tornando-a menos eficiente em certos contextos.