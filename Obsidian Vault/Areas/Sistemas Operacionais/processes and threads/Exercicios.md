## Retirados do livro -> Sistemas Operacionais Modernos (Andrew S. Tanenbaum, Herbert Bos) 4ª

## 23. A solução da espera ocupada usando a variável turn

A solução da espera ocupada usando a variável turn (Figura 2.23) funciona quando os dois processos estão executando em um multiprocessador de memória compartilhada, isto é, duas CPUs compartilhando uma memória comum?

Apesar de funcionar, não é adequado. A ideia de trabalhar com multiprocessador é que processos possam ser executados simultaneamente. Como a condição de alternância é forçada, um processo mais lento pode fazer um processo mais rápido ficar esperando. Além disso, um problema menor seria o desperdício de recurso para manter o próprio loop.

## 24. A solução de Peterson para o problema da exclusão mútua

A solução de Peterson para o problema da exclusão mútua mostrado na Figura 2.24 funciona quando o escalonamento de processos é preemptivo? E quando ele é não preemptivo?

A solução de Peterson adiciona um arranjo para garantir que o processo 0 só seja bloqueado quando, além de estar na vez do processo 1, o processo 1 esteja interessado. Temos mais uma camada de segurança. Para um escalonamento preemptivo, não há problemas, pois se o processo 0 for interrompido, não irá afetar a execução do processo 1. Já em um escalonamento não preemptivo, o desempenho pode ser prejudicado, pois se um processo permanecer por muito tempo na região crítica ou na execução de seu código não crítico antes de liberar a CPU, o outro processo será bloqueado por mais tempo.

## 28. Condição de corrida em simulações sequenciais

Sim, pois essas condições não dependem necessariamente de eventos simultâneos reais, mas da ordem em que as operações são executadas e acessam recursos compartilhados. As simulações podem testar diferentes intercalações de instruções de processos.

## 29. O problema produtor-consumidor

Sim, pois a solução dispõe de recursos como `empty` (garante que os produtores não adicionem itens quando o buffer está cheio), `full` (garante que os consumidores não tentem remover itens quando o buffer estiver vazio) e o `mutex` (garante que apenas um thread por vez tenha acesso à região crítica (buffer)). As variáveis, implementadas de forma sincronizada, garantem a exclusão mútua no acesso ao buffer e a sincronia de números de itens no buffer, impedindo operações inválidas.

## 30. Exclusão mútua com variável turn

A resposta é não. Podemos definir como pré-requisitos da exclusão mútua:

1. **Apenas um processo por vez pode estar na região crítica:** Atendido.
    
2. **Um processo fora da região crítica não pode impedir que outro entre:** Não atendido.
    
3. **Espera limitada:** Atendido.
    
4. **Independência da velocidade:** Não atendido.
    

## 31. Implementação de semáforos com desabilitação de interrupções

Um sistema operacional pode desabilitar interrupções temporariamente para suspender o atendimento de eventos enquanto executa operações críticas, garantindo a sincronização de semáforos.

## 32. Implementação de semáforos contadores com semáforos binários

```c
void down(semaphore *mutex, semaphore *block, int *count) {
    down(mutex);
    (*count)--;
    if (*count < 0) {
        up(mutex);
        down(block);
    } else {
        up(mutex);
    }
}
```

## 40. Processos duplicados em um escalonador circular

Se um processo aparecesse duas vezes na lista de processos executáveis, ele acabaria recebendo mais tempo de CPU, simulando prioridade mais alta sem alterar a lógica do escalonador.

## 41. Identificação de processos limitados por CPU ou E/S

Pode ser feita por análise do código-fonte e observação do comportamento em tempo de execução.

## 42. Quantum de tempo e chaveamento de contexto

- **Quantum curto:** Aumenta responsividade, mas aumenta overhead.
    
- **Quantum longo:** Reduz overhead, mas pode impactar processos interativos.
    

## 44. Ordem de execução para minimizar o tempo de resposta

A ordem de execução depende do valor de `X`. Para minimizar o tempo de resposta, deve-se seguir o algoritmo **Shortest Job First (SJF)**.

## 45. Cálculo do tempo de retorno médio para diferentes algoritmos

Para cada algoritmo, o tempo de retorno médio deve ser calculado considerando os tempos de execução e prioridades.

## 47. Escalonabilidade de chamadas de voz e vídeo

Com `U = 0.73`, o sistema é escalonável.

## 48. Inclusão de outro fluxo de vídeo

Com outro fluxo, `U = 1.06`, o que torna o sistema **não escalonável**.

## 50. Valor máximo de `x` para escalonabilidade

`x <= 12.5`.

## 52. Escalonabilidade de chamadas de voz e vídeo em sistema de tempo real

Com `U = 0.83`, o sistema **não é escalonável**.