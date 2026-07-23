---
tipo: conceito
area: Sistemas Operacionais
tags:
- so
criada: '2025-01-10'
---

## Memory sharing

**Explicação:** Em alguns sistemas operacionais, processos que estão trabalhando juntos podem compartilhar uma memória comum, que cada um pode ler e escrever. Essa memória compartilhada pode estar localizada na memória principal ou ser um arquivo compartilhado, e o local não altera a natureza da comunicação ou os problemas que surgem.

**Exemplo prático:** Um exemplo comum de comunicação entre processos é o spool de impressão. O processo que deseja imprimir um arquivo adiciona o nome do arquivo a um diretório especial de spool. Um daemon de impressão periodicamente verifica se há arquivos na fila para serem impressos, imprime-os e remove os nomes do diretório.

**Memória compartilhada no spool:** No exemplo do spool, imagine que o diretório tem várias vagas numeradas e há duas variáveis compartilhadas:

- **in:** Aponta para a próxima vaga livre.
- **out:** Aponta para o próximo arquivo a ser impresso.

Essas variáveis são compartilhadas por todos os processos que estão tentando adicionar arquivos à fila de impressão.
## Problema de concorrência e condições de corrida

**Situação problemática:** Imagine dois processos, A e B, tentando adicionar arquivos ao spool ao mesmo tempo:

- O processo A lê a variável **in** e armazena o valor 7 em sua variável local, acreditando que a vaga 7 é a próxima vaga livre.
- Antes de A conseguir escrever o nome do arquivo, ocorre uma interrupção e o processo B começa a executar.
- O processo B também lê o valor de **in** (7) e armazena o valor na sua própria variável local, acreditando que a próxima vaga livre também é 7.

**Consequência:**

- O processo B continua a execução, escreve seu arquivo na vaga 7 e atualiza **in** para 8.
- Mais tarde, o processo A retoma sua execução, escreve seu arquivo na vaga 7, apagando o arquivo de B, e também atualiza **in** para 8.
- O spool está agora consistente, mas o arquivo de B foi sobrescrito e o processo B nunca receberá a impressão.

## Condições de corrida

**Definição:** Essa situação, em que dois ou mais processos leem ou escrevem dados compartilhados ao mesmo tempo, e o resultado final depende da ordem de execução, é chamada de **condição de corrida**. Depurar programas com condições de corrida é difícil, pois os erros são intermitentes e difíceis de reproduzir.

**Impacto com o aumento do paralelismo:** Com o aumento do número de núcleos e o uso crescente de paralelismo, as condições de corrida estão se tornando mais comuns em sistemas modernos.

### Exclusão Mútua

Se um processo está usando uma variável ou arquivo compartilhado, os outros processos devem ser impedidos de acessá-lo até que o primeiro termine. A dificuldade ocorre porque processos podem interferir uns nos outros ao acessar dados compartilhados sem controle. Assim, é essencial usar mecanismos que garantam a exclusão mútua.

### Regiões Críticas

A parte do programa onde a memória compartilhada é acessada é chamada de **região crítica**. Para evitar condições de corrida, é necessário assegurar que dois processos nunca estejam em suas regiões críticas ao mesmo tempo.

### Como evitar? Para garantir a exclusão mútua, basta assegurar os 4 passos a seguir:

A chave para evitar condições de corrida é garantir que apenas um processo acesse os dados compartilhados por vez. Isso é alcançado por meio da **exclusão mútua**, que impede que múltiplos processos leiam ou escrevam simultaneamente na mesma memória ou arquivo compartilhado.

1 -  **Exclusividade:** Dois processos jamais podem estar simultaneamente dentro de suas regiões críticas.
2 -  **Independência de hardware:** Nenhuma suposição deve ser feita sobre velocidades ou quantidade de CPUs.
3 -  **Não interferência:** Um processo fora de sua região crítica não deve bloquear outros processos. OBS: isso ainda acontece na solução [[Mutual exclusion using Busy Wait|turn-based switching]].
4 -  **Evitar espera infinita:** Nenhum processo deve esperar eternamente para entrar em sua região crítica. OBS: Esse problema é resolvido nas soluções de [[Mutual exclusion using Busy Wait|Peterson e TSL]]

![[Pasted image 20241118141617.png]]