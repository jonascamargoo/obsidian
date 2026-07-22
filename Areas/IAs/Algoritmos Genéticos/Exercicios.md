---
tipo: conceito
area: IAs
tags:
- ia/algoritmos-geneticos
criada: '2025-06-10'
---

## 1 - Resuma o FGA em forma de passos

Um Algoritmo Genético (AG) opera em um ciclo evolutivo para encontrar soluções para problemas de busca e otimização. Os passos fundamentais são:

- **Passo 1: Inicialização da População:** Uma população inicial de _N_ indivíduos (cromossomos) é criada. Cada indivíduo representa uma solução candidata ao problema. Esta primeira geração é geralmente formada com valores aleatórios para garantir uma ampla diversidade inicial.
    
- **Passo 2: Avaliação (Fitness):** Cada indivíduo da população é avaliado por uma **função de avaliação (fitness)**. Essa função atribui uma pontuação que quantifica a qualidade da solução que o indivíduo representa. Soluções melhores recebem notas mais altas.
    
- **Passo 3: Seleção:** Indivíduos são selecionados da população atual para se tornarem "pais" da próxima geração. O critério de seleção é a aptidão: indivíduos com maior fitness têm maior probabilidade de serem escolhidos. Este processo é análogo à "sobrevivência dos mais aptos".

- **Passo 4: Operadores Genéticos (Recombinação e Mutação):** Os pais selecionados passam por **crossover** para combinar material genético e por **mutação** para introduzir novidades, gerando filhos.

## 2 - O que é a representação cromossomial?

A representação cromossomial é um componente crucial do AG, funcionando como a tradução do problema para uma estrutura que o computador possa manipular. A adequação dessa representação ao problema é diretamente proporcional à qualidade dos resultados, sendo essencial adaptar a representação ao problema e não o contrário. Cada parte indivisível dessa estrutura é chamada de gene. Embora a definição da representação seja flexível, ela deve seguir três regras gerais para ser eficaz: ser a mais simples possível, não permitir a representação de soluções inválidas e, sempre que possível, ter as restrições do problema embutidas em sua própria estrutura.

## 3 - Por que a população inicial é escolhida de forma aleatória?

É comum utilizar a inicialização dos indivíduos de forma aleatória porque essa abordagem geralmente garante uma boa **cobertura do espaço de busca**. Ao gerar soluções em pontos variados do domínio do problema, o algoritmo evita um viés inicial e aumenta as chances de que a população contenha a diversidade genética necessária para convergir para uma solução ótima global, em vez de ficar presa em um ótimo local.


## 4 - A única ligação entre o AG e o problema real é a função de avaliação. Por quê?

A única ligação entre o Algoritmo Genético e o problema real deve ser a função de avaliação, pois ela encapsula todos os objetivos e restrições do problema em um único valor de qualidade (fitness). Isso ocorre porque o AG é, em sua essência, um mecanismo de busca de propósito geral. Ele não "entende" o problema que está resolvendo; ele apenas manipula as representações (cromossomos) com o objetivo de maximizar a pontuação de fitness. Dessa forma, ao isolar o conhecimento do problema na função de avaliação, o AG pode ser aplicado a uma vasta gama de problemas sem que seu núcleo precise ser modificado. Além disso, implementado de forma orientada a objetos, torna-se ainda mais desacoplado do problema.

## 5 - Sobre convergência

### a) O que é convergência genética?

Convergência genética, ou convergência prematura, ocorre quando a população de um AG perde sua diversidade e a maioria dos indivíduos se torna muito semelhante ou idêntica. Isso faz com que o algoritmo estagne, concentrando sua busca em uma área limitada do espaço de soluções e perdendo a capacidade de explorar outras regiões potencialmente mais promissoras. Isso aproxima a solução de um mínimo ou máximo local.

### b) Como evitá-la na seleção dos pais?

Para evitar a convergência, é preciso controlar a **pressão seletiva** na seleção. Métodos como a **Seleção por Torneio** são eficazes, pois diminuem a chance de "superindivíduos" dominarem a população. Outra abordagem é a **Normalização Linear**, que ajusta os valores de fitness com base no ranking dos indivíduos, evitando que a seleção seja excessivamente gananciosa.

### c) Como determinar a convergência genética?

Determinar a ocorrência da convergência é uma tarefa fundamental, pois permite decidir entre parar a execução ou focar no operador de mutação para restaurar a variabilidade genética. É crucial que o cálculo dessa variabilidade seja feito com base no **genótipo** (a estrutura do cromossomo), e não na avaliação (fitness). A razão para isso é que indivíduos com genótipos muito diferentes podem apresentar avaliações parecidas; basear-se apenas nos valores de fitness poderia levar à conclusão incorreta de que a convergência ocorreu, quando na verdade ainda existe diversidade genética a ser explorada.

## 6) Sobre pontos de corte

### a) o que é ponto de corte?

Um ponto de corte é uma posição aleatória dentro de um cromossomo que serve como referência para a troca de material genético entre os pais durante o crossover.
### b) Exemplo para corte de um ponto

O crossover de um ponto seleciona um único ponto de corte. O material genético após esse ponto é trocado entre os dois pais para formar dois novos filhos.

1. **Seleção dos Pais:**
    
    - **Pai 1:** `[78.5, 0.01, 0.95]`
    - **Pai 2:** `[62.1, 0.5, 0.80]`
2. **Escolha do Ponto de Corte:** Vamos supor que o ponto de corte sorteado seja o índice 1 (a posição após o primeiro gene).
    
    - **Pai 1:** `[78.5 | 0.01, 0.95]`
    - **Pai 2:** `[62.1 | 0.5, 0.80]`
3. **Geração dos Filhos:** Agora, trocamos os segmentos que estão à direita do ponto de corte.
    
    - O **Filho 1** recebe a primeira parte do Pai 1 e a segunda parte do Pai 2.
    - O **Filho 2** recebe a primeira parte do Pai 2 e a segunda parte do Pai 1.
    
    O resultado é:
    
    - **Filho 1:** `[78.5, 0.5, 0.80]`
    - **Filho 2:** `[62.1, 0.01, 0.95]`

### c) Exemplo para corte de dois pontos

Da mesma forma, o crossover de dois pontos seleciona dois pontos de corte. O material genético _entre_ esses dois pontos é o que é trocado entre os pais.

1. **Seleção dos Pais (com mais genes para melhor ilustração):**
    
    - **Pai 1:** `[78.5, 0.01, 0.95, 120.0, 5.4]`
    - **Pai 2:** `[62.1, 0.5, 0.80, 99.0, 4.1]`
2. **Escolha dos Pontos de Corte:** Vamos supor que os pontos sorteados sejam o índice 1 e o índice 3.
    
    - **Pai 1:** `[78.5 | 0.01, 0.95, 120.0 | 5.4]`
    - **Pai 2:** `[62.1 | 0.5, 0.80, 99.0 | 4.1]`
3. **Geração dos Filhos:** Trocamos o segmento central.
    
    - O **Filho 1** recebe as "pontas" do Pai 1 e o "meio" do Pai 2.
    - O **Filho 2** recebe as "pontas" do Pai 2 e o "meio" do Pai 1.
    
    O resultado é:
    
    - **Filho 1:** `[78.5, 0.5, 0.80, 99.0, 5.4]`
    - **Filho 2:** `[62.1, 0.01, 0.95, 120.0, 4.1]`

### d) O que é o crossover baseado em maioria?

O **crossover baseado em maioria** é um operador de recombinação que utiliza múltiplos pais para gerar um único filho, em vez dos tradicionais dois pais. A sua principal característica é que o filho herda, para cada posição do cromossomo, o gene que é mais comum (majoritário) entre os pais selecionados.

Vamos supor que selecionamos **3 pais** para gerar um filho:

- **Pai 1:** `[ 1 | 0 | 1 | 1 | 0 | 1 ]`
- **Pai 2:** `[ 0 | 0 | 1 | 0 | 0 | 1 ]`
- **Pai 3:** `[ 1 | 1 | 1 | 0 | 1 | 1 ]`
- **Filho Gerado:** `[ 1 | 0 | 1 | 0 | 0 | 1 ]`

A principal razão para o uso restrito do crossover baseado em maioria é que ele **tende a acelerar a convergência do algoritmo de forma muito agressiva**. Ao promover apenas as características mais comuns, o operador elimina rapidamente as variações genéticas menos frequentes. Essa rápida perda de diversidade aumenta significativamente o risco de o algoritmo estagnar em uma solução boa, mas não ótima (um "ótimo local"), perdendo a capacidade de explorar outras áreas do espaço de busca.

## 7) Operador de mutação

### a) Qual é a sua importância?

A mutação é fundamental para **manter e introduzir diversidade genética** na população. Sua função é exploratória, garantindo que o algoritmo não estagne em ótimos locais e possa investigar novas áreas do espaço de busca.

### b) Variação da taxa de mutação

A taxa de mutação pode variar dinamicamente durante a execução. Uma estratégia comum é começar com uma taxa mais alta para garantir exploração e reduzi-la gradualmente para permitir o refinamento (convergência) em torno das melhores soluções encontradas.

## 8) Crossover vs Mutação

Embora a análise específica do autor não esteja disponível, a teoria geral indica que ambas as operações são cruciais, mas com funções distintas. O **crossover** é o principal operador de _explotação_, recombinando boas características já existentes, e por isso deve ser mais utilizado. A **mutação** é um operador de _exploração_, introduzindo novidades para evitar a estagnação. Portanto, o crossover é aplicado com alta frequência (taxa >70%), enquanto a mutação é usada de forma mais rara (taxa <1%). Nas pesquisas mais recentes, percebe-se uma importância maior da mutação.

## 9) Seleção Natural

### a) O que é pressão seletiva?
É a força que impulsiona a população em direção a soluções de maior qualidade. Ela define o quão rigorosa é a seleção, ou seja, o grau de vantagem que os indivíduos mais aptos têm para se reproduzir.

### b) O que é intensidade de seleção
É a medida quantitativa da pressão seletiva. Uma alta intensidade acelera a convergência, selecionando apenas os melhores indivíduos. Uma baixa intensidade retarda a convergência, mas ajuda a manter a diversidade genética ao permitir que indivíduos de menor fitness também se reproduzam.

### c) Método de torneio

Neste método, _t_ indivíduos são sorteados aleatoriamente, e o melhor deles é selecionado. O tamanho do torneio (_t_) controla a pressão seletiva de forma eficiente. É um método robusto que evita os principais problemas da roleta, sendo amplamente utilizado.

## 10) Problemas flutuantes (reais)

A questão apresenta um problema com indivíduos de genes flutuantes (valores reais) e nos pede para aplicar e explicar operadores genéticos específicos para essa representação.

**Pais do Problema:**

- **Pai 1 (P1):** `[57.0, 60.0]`
- **Pai 2 (P2):** `[53.0, 56.0]`

### (a) Recombinação Detalhada

A recombinação (ou crossover) visa criar um ou mais filhos combinando as características dos pais.

#### i. Recombinação Aritmética

Este é o método de recombinação mais intuitivo para valores reais. Ele cria um ou mais filhos que são uma **combinação linear** dos pais. A fórmula geral para um filho é:

`Filho = α * P1 + (1 - α) * P2`

Onde `α` (alfa) é um fator de ponderação sorteado aleatoriamente, geralmente no intervalo `[0, 1]`.

**Cálculo Passo a Passo (usando α = 0.5 para uma média simples):**

Para gerar um filho, aplicamos a fórmula a cada gene individualmente:

- **Cálculo para o Gene 1:**
    
    - `gene1_filho = 0.5 * P1[gene1] + 0.5 * P2[gene1]`
    - `gene1_filho = 0.5 * 57.0 + 0.5 * 53.0`
    - `gene1_filho = 28.5 + 26.5 = 55.0`
- **Cálculo para o Gene 2:**
    
    - `gene2_filho = 0.5 * P1[gene2] + 0.5 * P2[gene2]`
    - `gene2_filho = 0.5 * 60.0 + 0.5 * 56.0`
    - `gene2_filho = 30.0 + 28.0 = 58.0`

**Resultado:** O filho gerado pela média aritmética dos pais é **`[55.0, 58.0]`**. Este filho representa uma solução intermediária, localizada exatamente entre os dois pais no espaço de busca.

#### ii. Recombinação BLX-α (Blend Crossover)

Este método é mais exploratório. Em vez de gerar um ponto fixo, ele define um **intervalo** em torno dos genes dos pais e sorteia um novo valor dentro desse intervalo. O `α` aqui controla o tamanho dessa "folga" no intervalo.

A fórmula para o intervalo de cada gene é: `[min - I*α, max + I*α]`

**Cálculo Passo a Passo (usando α = 0.5):**

- **Cálculo para o Gene 1 (Valores dos pais: 53.0 e 57.0):**
    
    1. **Identificar `min` e `max`**: `min = 53.0`, `max = 57.0`.
    2. **Calcular a distância `I`**: `I = max - min = 57.0 - 53.0 = 4.0`.
    3. **Calcular a folga**: `folga = I * α = 4.0 * 0.5 = 2.0`.
    4. **Definir o intervalo final**: `[min - folga, max + folga] = [53.0 - 2.0, 57.0 + 2.0] = [51.0, 59.0]`.
    5. O novo gene 1 do filho será um **número aleatório** sorteado de forma uniforme dentro do intervalo `[51.0, 59.0]`.
- **Cálculo para o Gene 2 (Valores dos pais: 56.0 e 60.0):**
    
    1. **Identificar `min` e `max`**: `min = 56.0`, `max = 60.0`.
    2. **Calcular a distância `I`**: `I = max - min = 60.0 - 56.0 = 4.0`.
    3. **Calcular a folga**: `folga = I * α = 4.0 * 0.5 = 2.0`.
    4. **Definir o intervalo final**: `[min - folga, max + folga] = [56.0 - 2.0, 60.0 + 2.0] = [54.0, 62.0]`.
    5. O novo gene 2 do filho será um **número aleatório** sorteado de forma uniforme dentro do intervalo `[54.0, 62.0]`.

**Resultado:** O filho gerado pelo BLX-α não é fixo. Poderia ser, por exemplo, `[53.4, 61.1]` ou `[58.9, 55.2]`, dependendo dos números aleatórios sorteados nos intervalos calculados.

---

### (b) Mutação Gaussiana Detalhada

A mutação gaussiana é o operador de mutação padrão para genes de valores reais. Sua função é introduzir uma pequena variação em um gene existente, como um ajuste fino.

#### Como Ocorre a Mutação

Ela funciona somando a um gene um número aleatório retirado de uma **distribuição Normal (ou Gaussiana)**.

A fórmula é simples: `gene_mutado = gene_original + Z`

Onde `Z` é a variável aleatória de distribuição normal.

#### Como a Variável Aleatória é Calculada

Essa variável `Z` é definida por dois parâmetros:

1. **Média (`μ`):** É definida como **`μ = 0`**. Isso é fundamental, pois garante que a mutação não tem um viés. A alteração tem a mesma probabilidade de aumentar ou diminuir o valor do gene.
2. **Desvio Padrão (`σ`):** É um parâmetro definido pelo programador. Ele controla a **magnitude** da mutação.
    - Um **`σ` pequeno** (ex: 0.1) fará com que os valores de `Z` sejam quase sempre muito próximos de zero, resultando em mutações muito sutis (ajuste fino).
    - Um **`σ` grande** (ex: 10.0) permitirá que `Z` assuma valores mais distantes de zero, causando mutações maiores e mais exploratórias