
## Handling cache misses (data and instruction)

O processamento de cache miss gera um stall, ao contrário de uma interrupção, que exigiria salvar o estado de todos os registradores. Para um cache miss, podemos parar todo o processador, essencialmente congelando o conteúdo dos registradores temporários e visíveis ao programador, enquanto aguardamos. Processadores mais sofisticados, que operam fora de ordem, podem permitir a execução de instruções enquanto aguardam por uma falta de cache.

Vamos examinar mais de perto como as faltas de instrução são tratadas; a mesma abordagem pode ser facilmente estendida para lidar com faltas de dados. Se um acesso a uma instrução resultar em um miss, o conteúdo do registrador de instrução se torna inválido. Para obter a instrução correta na cache, precisamos instruir o nível inferior na hierarquia de memória a realizar uma leitura. Como o PC counter é incrementado no primeiro ciclo de clock de execução, o endereço da instrução que gera uma falta na cache de instrução é igual ao valor do contador de programa menos 4. Depois de obtermos o endereço, precisamos instruir a memória principal a realizar uma leitura. Aguardamos a resposta da memória (pois o acesso levará vários ciclos de relógio) e, em seguida, escrevemos as words contendo a instrução desejada na cache. O step-by-step:

1. Envie o valor original do PC (PC atual - 4) para a memória.
2. Instrua a memória principal a realizar uma leitura e aguarde a conclusão do acesso pela memória.
3. Escreva a entrada da cache, colocando os dados da memória na parte de dados da entrada, escrevendo os bits superiores do endereço (da ALU) no campo de tag e ativando o bit de válido.
4. Reinicie a execução da instrução no primeiro passo, o que buscará novamente a instrução, encontrando-a desta vez na cache e saindo do stall.

## Handling writes

Writes funcionam de maneira um pouco diferente. Suponha, em uma instrução de store, escrevemos os dados apenas na cache de dados (sem alterar a memória principal); então, após a escrita na cache, a memória teria um valor diferente do que está na cache. Nesse caso, diz-se que a cache e a memória estão inconsistentes. A maneira mais simples de manter a memória principal e a cache consistentes é sempre escrever (write-through).

### Write-through

Esquema o qual, em escritas, tanto a cache e o próximo nível mais baixo de memória são atualizados, garantindo que os dados estejam sempre consistentes.  Solução simples, mas ineficiente.

#### Quando ocorre um write miss?

Vamos supor uma situação a qual tentamos escrever em um byte que não está presente no bloco. Primeiro, buscamos as palavras do bloco na memória. Após realizar o fetch do bloco e o ter  colocado na cache, podemos sobrescrever a palavra que causou a falha no bloco da cache. Também escrevemos a palavra na memória principal usando o endereço completo.

### Write buffer

Um write buffer armazena os dados enquanto aguarda para serem gravados na memória. Após escrever os dados na cache e no buffer de escrita, o processador pode continuar a execução. Quando uma gravação na memória principal é concluída, a entrada no buffer de escrita é liberada. Se o buffer de escrita estiver cheio quando o processador chegar a uma operação de escrita, o processador precisará aguardar (stall) até que haja uma posição vazia no buffer de escrita. Claro, se a taxa com que a memória pode concluir as gravações for menor do que a taxa com que o processador está gerando gravações, nenhum volume de armazenamento em buffer pode ajudar, porque as gravações estão sendo geradas mais rapidamente do que o sistema de memória pode aceitá-las. Step-by-step:

1. **Início:**
    - O processador executa uma instrução de escrita que precisa ser gravada na memória.
2. **Verificação do Buffer:**
    - Antes de escrever diretamente na memória, o processador verifica se há espaço disponível no buffer de escrita.
3. **Escrita no Buffer:**
    - Se houver espaço, o dado a ser escrito é colocado no buffer de escrita.
4. **Continuação da Execução:**
    - O processador pode continuar executando outras instruções sem esperar pela conclusão da gravação na memória.
5. **Assincronia:**
    - A transferência real dos dados do buffer de escrita para a memória pode ocorrer de maneira assíncrona. Isso significa que o processador não precisa aguardar a conclusão da gravação para continuar suas operações.
6. **Escrita na Memória:**
    - Em algum ponto, os dados armazenados no buffer de escrita são transferidos para a memória principal. Isso pode ser feito em lotes ou conforme a política de gerenciamento do buffer.
7. **Liberar Entradas:**
    - Após a conclusão da gravação na memória, as entradas correspondentes no buffer de escrita são liberadas.
8. **Gestão de Substituição:**
    - Se o buffer estiver cheio quando uma nova escrita ocorrer, pode ser necessário substituir ou descartar dados no buffer. Isso geralmente segue alguma estratégia de substituição, como a política FIFO (primeiro a entrar, primeiro a sair) ou outras políticas de gerenciamento.

### Write back

Uma possível alternativa para o write-through é o write back. Em um esquema de escrita adiada (write-back), quando uma operação de escrita ocorre, o novo valor é gravado apenas no bloco da cache. O bloco modificado é escrito no nível mais baixo da hierarquia quando é substituído. Esquemas de escrita adiada podem melhorar o desempenho, especialmente quando os processadores conseguem gerar operações de escrita tão rápido ou mais rápido do que as escritas podem ser tratadas pela memória principal; entretanto, um esquema de escrita adiada é mais complexo de implementar do que um esquema de escrita direta. Exemplo de step-by-step:

1. **Início:**
    - O processador executa uma instrução de escrita que precisa ser gravada na memória.
2. **Verificação da Cache:**
    - O processador verifica se o bloco de memória que contém os dados a serem gravados está na cache.
3. **Leitura da Cache:**
    - Se o bloco estiver na cache, ele é lido para obter a versão mais recente dos dados.
4. **Atualização na Cache:**
    - O novo valor é escrito apenas no bloco da cache, indicando que o bloco foi modificado.
5. **Continuação da Execução:**
    - O processador pode continuar executando outras instruções sem esperar pela conclusão da gravação na memória.
6. **Marcação do Bloco como Modificado:**
    - O bloco modificado na cache é marcado para indicar que os dados foram alterados desde a última leitura.
7. **Substituição do Bloco:**
    - Quando o bloco modificado é removido da cache (por exemplo, devido à política de substituição), ele é escrito de volta para a memória principal.
8. **Escrita na Memória:**
    - O bloco modificado é escrito no nível mais baixo da hierarquia de memória, atualizando assim a versão na memória principal.
9. **Liberar Entradas:**
    - As entradas correspondentes na cache são liberadas para futuras operações de leitura e escrita.

