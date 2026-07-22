---
tipo: conceito
area: IAs
tags:
- ia/algoritmos-geneticos
criada: '2025-06-10'
---

## 1. Introdução aos Algoritmos Genéticos

Algoritmos Genéticos (AGs) são algoritmos matemáticos e probabilísticos inspirados no princípio darwiniano da evolução das espécies e na genética. Eles constituem uma técnica de busca e otimização, altamente paralela, que fornece um mecanismo de busca adaptativa baseado no princípio de sobrevivência dos mais aptos e na reprodução.

Eles fazem parte de uma área maior da ciência chamada **Inteligência Computacional**, que busca desenvolver sistemas inteligentes imitando aspectos do comportamento humano e da natureza, como aprendizado, percepção, raciocínio, evolução e adaptação.

### 1.1. Princípios Fundamentais

Os princípios da natureza que inspiram os AGs são simples. De acordo com a teoria de Charles Darwin, o princípio da seleção natural privilegia os indivíduos mais aptos, que tendem a ter maior longevidade e, consequentemente, maior probabilidade de reprodução. Indivíduos que geram mais descendentes têm uma chance maior de perpetuar seus códigos genéticos nas gerações futuras.

Esses princípios são imitados computacionalmente para buscar uma solução melhor para um determinado problema, através da evolução de uma população de soluções codificadas.

### 1.2. Analogia Biológica

Para entender o funcionamento de um AG, é fundamental conhecer a analogia entre seus componentes e os termos da genética clássica.

|Termo na Natureza|Termo no Algoritmo Genético|Descrição|
|:--|:--|:--|
|Indivíduo|**Solução**|Uma das possíveis soluções para o problema em questão.|
|Cromossomo|**Cromossomo / Estrutura de Dados**|Estrutura de dados que representa uma solução. Pode ser um vetor, uma palavra binária, etc.|
|Gene|**Gene**|Uma parte indivisível do cromossomo, que representa uma característica do problema.|
|Alelo|**Valor do Gene**|O valor específico que um gene assume.|
|Loco|**Posição do Gene**|A posição do gene dentro da estrutura do cromossomo.|
|Genótipo|**Estrutura (Genótipo)**|A estrutura de dados completa que codifica a solução.|
|Fenótipo|**Solução Decodificada (Fenótipo)**|A solução real do problema, obtida após a decodificação do genótipo.|
|Geração|**Ciclo / Iteração**|Um ciclo do algoritmo, onde uma nova população é gerada.|


## 2. Componentes de um Algoritmo Genético

Um Algoritmo Genético pode ser caracterizado pelos seguintes componentes principais:

1. **Representação das Soluções (Codificação)**
2. **Inicialização da População**
3. **Função de Avaliação (Fitness)**
4. **Seleção**
5. **Operadores Genéticos (Crossover e Mutação)**
6. **Critérios de Parada e Parâmetros**

O fluxo geral de um AG pode ser visualizado no diagrama abaixo, onde ciclos de avaliação, seleção e reprodução (com operadores genéticos) se repetem até que um critério de parada seja atingido.

### 2.1. Representação Cromossomial (Genótipo)

A representação é a maneira de traduzir a informação de um problema em uma estrutura de dados que o AG possa manipular. A escolha da representação é crucial e depende do tipo de problema a ser resolvido. Ela deve ser capaz de representar todo o espaço de busca desejado.

**Regras para uma boa representação:**

- **Simplicidade:** A representação deve ser a mais simples possível.
- **Validade:** Soluções proibidas (inválidas) não devem ter uma representação.
- **Totalidade:** Condições e restrições do problema devem estar, se possível, implícitas na representação.

Os principais tipos de representação são:

|Representação|Problemas Comuns|
|:--|:--|
|**Binária**|Numéricos, Inteiros|
|**Números Reais**|Numéricos|
|**Permutação de Símbolos**|Baseados em Ordem (ex: Caixeiro Viajante)|
|**Símbolos Repetidos**|Agrupamento|

Exportar para as Planilhas

A **representação binária** é a mais tradicional e simples. Nela, o cromossomo é uma sequência de bits. Sua principal vantagem é a facilidade de manipulação pelos operadores genéticos e a simplicidade na prova de teoremas.

Embora simples, a representação binária nem sempre é a mais adequada, pois alguns problemas exigem um alfabeto com mais símbolos. A representação por **números reais** (ponto flutuante), por exemplo, pode oferecer um melhor desempenho em certos casos.

### 2.2. Decodificação

A decodificação é o processo de converter o genótipo (a representação) em um fenótipo (a solução real do problema) para que ela possa ser avaliada.

Na representação binária, a transformação para um número inteiro é direta. Para converter um binário em um número real X_R dentro de um intervalo [X_min,X_max], pode-se usar a seguinte fórmula:

XR​=Xmin​+Xb×2n−1C​

Onde:

- Xb é o valor inteiro correspondente ao binário.
- n é o número de bits do cromossomo.
- C é o comprimento do domínio, dado por C=∣X_max−X_min∣.
    

### 2.3. Inicialização da População

Este processo cria a primeira geração de indivíduos (soluções).

- **Inicialização Aleatória:** É a abordagem mais comum. A população inicial é formada por indivíduos gerados aleatoriamente. Isso geralmente garante uma boa cobertura do espaço de busca.
    
- **Inicialização com Sementes (Seeding):** Se já se conhece a priori algumas boas soluções ou características, a população inicial pode ser "semeada" com esses cromossomos para acelerar a convergência.
    
- **Particionamento do Espaço:** Uma técnica é dividir o espaço de busca em k subespaços e gerar n/k indivíduos em cada um, garantindo uma distribuição mais uniforme das soluções iniciais.

### 2.4. Função de Avaliação (Fitness)

A função de avaliação, ou _fitness_, é o elo entre o AG e o problema real. Ela mede a qualidade de um indivíduo, ou seja, quão boa é a solução que ele representa. Essa "nota" é fundamental para guiar o processo de busca, diferenciando soluções boas de ruins.

A função deve ser desenhada com cuidado, embutindo o máximo de conhecimento sobre os objetivos e restrições do problema. Como os AGs são, por padrão, algoritmos de maximização, a função deve retornar um valor maior para soluções melhores.

**Exemplo de Código para Função de Avaliação:** O código a seguir mostra um exemplo prático. Primeiro, a rotina `converteBooleano` decodifica partes de um cromossomo binário. Em seguida, `calculaAvaliacao` usa esses valores decodificados para calcular a nota de fitness da solução.

Java

```
// Converte um trecho da string binária para um número
public float converteBooleano(int inicio, int fim) {
    String s = this.getValor();
    float aux = 0;
    for (int i = inicio; i <= fim; i++) {
        aux *= 2;
        if (s.substring(i, i + 1).equals("1")) {
            aux += 1;
        }
    }
    return aux;
}

// Calcula a nota (avaliação) do indivíduo
public double calculaAvaliacao() {
    // Decodifica os valores x e y do cromossomo
    double x = this.converteBooleano(0, 21);
    double y = this.converteBooleano(22, 43);
    
    // Mapeia os valores para o intervalo desejado, ex: [-100, 100]
    x = 0.00004768372718899898 * x - 100;
    y = 0.00004768372718899898 * y - 100;
    
    // Calcula a função objetivo, ex: |x*y*sin(y*pi/4)|
    this.avaliacao = Math.abs(x * y * Math.sin(y * Math.PI / 4));
    return this.avaliacao;
}
```

## 3. Seleção

O processo de seleção escolhe quais indivíduos da população atual serão selecionados para a reprodução. A seleção é baseada na aptidão (fitness) dos indivíduos: os mais aptos têm maior probabilidade de serem escolhidos. A forma como a seleção é implementada define a **pressão seletiva** do algoritmo — a força que impulsiona as melhores soluções para as gerações seguintes.

### 3.1. Métodos de Seleção

Existem vários mecanismos de seleção. Os cinco principais são: proporcional (roleta), torneio, truncamento, normalização linear e normalização exponencial.

#### Seleção Proporcional (Roleta Viciada)

Neste método, cada indivíduo recebe uma fatia de uma "roleta" proporcional à sua aptidão. A probabilidade p_i de um indivíduo i ser selecionado é a razão entre sua aptidão f_i e a soma das aptidões de toda a população:

pi​=∑j=1N​fj​fi​​

**Problemas da Seleção Proporcional:**

- **Superindivíduos:** Um indivíduo com uma aptidão muito superior aos demais pode dominar a roleta, levando a uma convergência prematura do algoritmo.
    
- **Estagnação (Competição Próxima):** Quando todos os indivíduos têm aptidões muito semelhantes, a intensidade da seleção se torna muito baixa, quase aleatória.
    
- **Avaliações Negativas:** O método não funciona nativamente com valores de fitness negativos, exigindo escalonamento ou normalização dos dados.

#### Seleção por Torneio

Neste método, um grupo de t indivíduos é escolhido aleatoriamente da população, e o indivíduo com a melhor aptidão dentro desse grupo é selecionado. O tamanho do torneio (t) é um parâmetro chave: quanto maior o t, maior a pressão seletiva. Esta técnica lida melhor com superindivíduos, pois mesmo o melhor indivíduo da população não tem garantia de ser escolhido para um torneio.

#### Seleção por Truncamento

É um método simples onde apenas os T melhores indivíduos da população são selecionados para reprodução. Cada um desses indivíduos selecionados tem a mesma probabilidade de se reproduzir.

#### Seleção por Normalização Linear

Para contornar os problemas da seleção proporcional, este método ordena os indivíduos por sua aptidão e, em seguida, atribui-lhes novos valores de fitness de acordo com sua posição (ranking) na ordenação. Os novos valores são distribuídos linearmente entre um `mín` e um `máx` definidos pelo usuário. Isso reduz o domínio de superindivíduos e aumenta a pressão seletiva entre indivíduos com avaliações próximas.

#### Seleção por Normalização Exponencial

Similar à normalização linear, mas as probabilidades de seleção seguem uma função exponencial, o que pode dar um controle mais fino sobre a pressão seletiva.

## 4. Operadores Genéticos

Após a seleção, os indivíduos escolhidos (pais) passam por operadores genéticos para criar novos indivíduos (filhos). Os operadores genéticos se classificam em recombinação (crossover), mutação e inversão.

### 4.1. Crossover (Recombinação)

O crossover é considerado a característica fundamental dos AGs. Ele combina o material genético de dois pais para criar um ou mais descendentes. Os filhos herdarão características de ambos os genitores.

- **Crossover de Um Ponto:** Uma posição de corte é escolhida aleatoriamente no cromossomo, e os pais trocam os segmentos após esse ponto para gerar dois filhos.
    
- **Crossover de Dois Pontos:** Dois pontos de corte são escolhidos. O material genético entre os dois pontos é trocado entre os pais. Este operador é capaz de combinar _schemata_ com posições fixas nas extremidades.
    
- **Crossover Uniforme:** Para cada gene do filho, sorteia-se de qual dos pais ele será herdado, geralmente com 50% de chance para cada. Este operador utiliza um padrão binário para designar os bits de cada genitor. Embora poderoso para recombinar quaisquer posições, ele tem um poder de destruição de padrões maior que os crossovers de um e dois pontos. Por isso, seu uso é mais indicado em ambientes elitistas, que garantem a sobrevivência dos melhores indivíduos.
    
- **Crossover Baseado em Maioria:** Sorteiam-se n pais e cada bit do filho é definido pelo valor que aparece na maioria dos pais naquela posição. Tende a acelerar a convergência.

### 4.2. Mutação

A mutação é um operador exploratório que tem como objetivo aumentar a diversidade genética da população, evitando a convergência prematura. Ela atua alterando aleatoriamente o valor de um ou mais genes de um cromossomo. A probabilidade de mutação (p_m) costuma ser muito baixa (ex: &lt; 1%).

- **Taxa de mutação muito baixa:** A população perde diversidade e estagna.
- **Taxa de mutação muito alta:** O AG se descaracteriza e passa a se comportar como uma busca aleatória.

### 4.3. Inversão

É um operador que troca a posição de dois genes escolhidos aleatoriamente. Sua importância é mais restrita a problemas onde a ordem dos genes é fundamental (problemas de permutação).

## 5. Dinâmica da População (Seleção de Sobreviventes)

As técnicas de reprodução (ou seleção de sobreviventes) determinam como a nova população é formada e quais indivíduos da geração antiga são substituídos.

- **Troca de Toda a População (Modelo Geracional):** A cada ciclo, todos os N indivíduos da população são substituídos por N novos descendentes.
    
- **Troca com Elitismo:** Similar ao anterior, mas o melhor indivíduo da população corrente é copiado diretamente para a próxima geração, garantindo que a melhor solução encontrada até o momento nunca seja perdida.
    
- **Troca Parcial (Steady-State):** A cada ciclo, apenas um pequeno número M de indivíduos ($M\) é gerado, e eles substituem os M piores indivíduos da população corrente. Este modelo mantém a população mais estática, permitindo o uso de operadores como o crossover uniforme. Uma variação impede a presença de indivíduos duplicados na população para garantir um melhor aproveitamento do paralelismo do AG.
    

## 6. Parâmetros e Critérios de Parada

Vários parâmetros controlam o processo evolucionário de um AG.

- **Tamanho da População:** Número de soluções avaliadas em paralelo a cada ciclo.
    
- **Taxa de Crossover (p_c):** Probabilidade de um par de indivíduos selecionados sofrer recombinação.
    
- **Taxa de Mutação (p_m):** Probabilidade de um gene sofrer mutação.
    
- **Critério de Parada:** Geralmente, o algoritmo para após um **Número de Gerações** pré-definido ou quando a melhor solução não apresenta melhora por um certo número de ciclos.
    

A escolha desses parâmetros é empírica e depende do problema. É possível usar técnicas de **interpolação de parâmetros**, onde as taxas (de mutação, por exemplo) são ajustadas dinamicamente durante a execução, de forma linear ou adaptativa (com base no desempenho dos operadores).

## 7. Fundamentos Matemáticos: A Teoria de Schemata

Para entender _por que_ os AGs funcionam, John Holland desenvolveu a **Teoria de Schema**.

- **Schema (plural: schemata):** É um padrão que descreve um conjunto de cromossomos com similaridades em certas posições. Utiliza-se um símbolo adicional `*` (ou `Σ`) que funciona como um "não importa" (_don't care_). Por exemplo, o schema `H = 1*1*0` representa todos os cromossomos de 5 bits que começam com `1`, têm `1` na terceira posição e `0` na quinta.
    

O **Teorema Fundamental dos Algoritmos Genéticos** afirma que:

> "Schemata curtos, de baixa ordem e com aptidão acima da média recebem um número exponencialmente crescente de representantes nas gerações seguintes."

Isso significa que o AG não processa soluções individuais, mas sim um número massivo de padrões (schemata) em paralelo. Ele implicitamente dá mais "testes" aos padrões que se provaram mais promissores (com fitness acima da média), combinando-os através do crossover para formar novas soluções potencialmente ainda melhores.

- Schemata com aptidão acima da média da população tendem a proliferar.
    
- Schemata com aptidão abaixo da média tendem a desaparecer.
    

O crossover tende a quebrar schemata longos (com grande distância entre suas posições fixas), enquanto a mutação pode quebrar qualquer schema. É por isso que padrões **curtos** e de **baixa ordem** (poucas posições fixas) têm maior probabilidade de sobreviver e se propagar.

## 8. Aplicações

AGs são particularmente úteis para problemas de otimização complexos, como:

- Problemas com muitos parâmetros e grande espaço de busca.
- Problemas com restrições difíceis de modelar matematicamente.
- Otimização de Funções, Otimização Combinatorial (ex: Problema do Caixeiro Viajante), Otimização de Planejamento e Roteamento de Veículos.
    

Exemplos de aplicações práticas incluem:

- Previsão e Suporte à Decisão.
    
- Otimização em Negócios e Finanças (Fluxo de Caixa, Análise de Investimentos).
    
- Engenharia (Síntese e Layout de Circuitos Eletrônicos, Otimização de Distribuição de Energia).
    
- Logística (Planejamento de Embarque, Alocação de Espaço Físico).
    
- Mineração de Dados (_Data Mining_) para classificação de clientes.