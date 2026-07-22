---
tags:
  - otimização
  - teoria-da-decisao
  - tomada-de-decisao
  - CEFET-MG
aliases:
  - Teoria da Decisão
  - Análise de Decisão
---

# Teoria da Decisão

## Definição

A tomada de decisão é o ato de selecionar uma opção entre duas ou mais alternativas disponíveis. Esse processo é fundamentado em objetivos, valores, informações e, em certos casos, intuições. Envolve deliberação, julgamento e o comprometimento com a escolha feita.

## Elementos Comuns em Problemas de Decisão

Todo problema de decisão, independentemente de sua complexidade, possui três elementos comuns:
- **Estratégias alternativas**: Correspondem aos cursos de ação ou possíveis soluções para o problema. Cada alternativa leva a um resultado distinto.
- **Estados da natureza**: São os eventos futuros sobre os quais o tomador de decisão não tem controle, mas que influenciam os resultados das alternativas.
- **Resultados**: Representam a consequência de escolher uma determinada alternativa quando ocorre um específico estado da natureza[.

## Tipos de Decisão

As decisões podem ser classificadas de acordo com a base principal utilizada no processo de escolha.

- **Racional**: Baseia-se em análise lógica e dados objetivos. É um processo estruturado que compara alternativas e avalia consequências para atender a critérios definidos.
- **Intuitiva**: Guiada por sentimentos, experiências ou instintos, sem uma análise lógica detalhada. O cérebro acessa rapidamente experiências passadas para chegar a uma conclusão quase automática.
- **Impulsiva**: Realizada rapidamente, com base em emoções intensas e sem reflexão sobre as consequências
- **Estratégica**: Focada no longo prazo, com planejamento e impacto significativo sobre objetivos maiores.

## Ambientes de Tomada de Decisão

A tomada de decisão pode ocorrer em diferentes contextos, definidos pelo nível de conhecimento sobre os estados da natureza.

### 1. Decisão sob Condição de Certeza
Neste ambiente, o tomador de decisão conhece previamente o resultado de cada alternativa. As informações sobre os resultados são precisas, mensuráveis e confiáveis.

### 2. Decisão sob Condição de Risco
Ocorre quando as probabilidades de ocorrência de cada estado da natureza são conhecidas. A decisão é fundamentada no resultado médio ou esperado de cada alternativa.
- O risco, segundo Gerd Gigerenzer, existe quando todas as alternativas relevantes, suas consequências e as probabilidades de ocorrência são conhecidas.

### 3. Decisão sob Condição de Incerteza
Neste cenário, os possíveis estados da natureza são conhecidos, mas não há estimativas sobre suas probabilidades de ocorrência.
- A incerteza, segundo Gigerenzer, ocorre quando não se conhecem todas as alternativas, suas consequências ou suas probabilidades.

## Ferramentas e Critérios para Análise de Decisão

### Matriz de Decisão
É uma ferramenta gerencial que permite visualizar as estratégias alternativas, os estados da natureza e os resultados associados. Os resultados são geralmente expressos numericamente, como lucros, custos ou tempo.

A estrutura geral é a seguinte:

| Alternativas |  $EN_1$  |  $EN_2$  | ... |  $EN_k$  |
| :----------- | :------: | :------: | :-: | :------: |
| $A_1$        | $R_{11}$ | $R_{12}$ | ... | $R_{1k}$ |
| $A_2$        | $R_{21}$ | $R_{22}$ | ... | $R_{2k}$ |
| ...          |   ...    |   ...    | ... |   ...    |
| $A_p$        | $R_{p1}$ | $R_{p2}$ | ... | $R_{pk}$ |

### Critérios para Decisão sob Risco

#### Valor Esperado da Alternativa (VEA)
O VEA é a média ponderada dos resultados de cada alternativa, usando as probabilidades dos estados da natureza como pesos.
- **Fórmula**: `VEA(Ai) = Σ [Resultado(ij) * Probabilidade(j)]`
- **Decisão**:
    -  Se os resultados forem lucros ou receitas, escolhe-se a alternativa com o **maior** VEA.
    - Se os resultados forem custos ou despesas, escolhe-se a alternativa com o **menor** VEA.

#### Valor Esperado da Informação Perfeita (VEIP)
O VEIP mede o ganho adicional que seria obtido se conhecêssemos de antemão qual estado da natureza ocorreria. Representa o preço máximo que um tomador de decisão estaria disposto a pagar por informações perfeitas.
- **Cálculo**:
    1. Para cada estado da natureza, identificar o melhor resultado possível entre todas as alternativas.
    2. Calcular o valor esperado com informação perfeita (VECIP), que é a média ponderada desses melhores resultados.
    3. Subtrair o maior VEA (calculado anteriormente) do VECIP. 
    - `VEIP = VECIP - max(VEA)`

#### Análise de Sensibilidade
Avalia o impacto na decisão final caso haja variações nos valores dos resultados ou nas probabilidades dos estados da natureza. Permite identificar o ponto de indiferença, onde a escolha entre duas alternativas se equivale.

#### Árvore de Decisão
É uma representação gráfica do problema de decisão que auxilia na visualização das alternativas, probabilidades e consequências. A árvore é lida da esquerda para a direita e é composta por:
- **Nós de Decisão**: Pontos onde uma escolha deve ser feita.
- **Nós de Incerteza/Estado da Natureza (○)**: Pontos que representam os eventos aleatórios e suas probabilidades.
- **Ramos**: Linhas que conectam os nós, representando as alternativas ou os estados da natureza.

### Critérios para Decisão sob Incerteza

Como as probabilidades são desconhecidas, a escolha do critério depende do perfil do tomador de decisão (otimista, pessimista, etc.).

- **Critério Maximax (Otimista)**: Para cada alternativa, seleciona-se o melhor resultado possível. Em seguida, escolhe-se a alternativa que oferece o maior desses melhores resultados.

- **Critério Maximin (Pessimista)**: Para cada alternativa, identifica-se o pior resultado. Depois, escolhe-se a alternativa que corresponde ao melhor desses piores resultados.

- **Critério de Laplace (Igualmente Provável)**: Assume que todos os estados da natureza têm a mesma probabilidade de ocorrer. Calcula-se a média aritmética simples dos resultados para cada alternativa e escolhe-se aquela com a melhor média.

- **Critério do Realismo de Hurwicz**: Um meio-termo entre o otimismo e o pessimismo, utilizando um coeficiente de otimismo `α` (alfa), onde `0 ≤ α ≤ 1`.
    - `α = 1` representa um tomador de decisão totalmente otimista (Maximax).
    - `α = 0` representa um tomador de decisão totalmente pessimista (Maximin).
    - **Cálculo**: Para cada alternativa, calcula-se uma média ponderada: `[Melhor Resultado * α] + [Pior Resultado * (1-α)]`. Escolhe-se a alternativa com o maior valor ponderado.

- **Critério do Mínimo Arrependimento (Savage)**: O objetivo é minimizar o arrependimento, que é a perda por não ter escolhido a melhor alternativa para um estado da natureza que de fato ocorreu
    1. Criar uma "matriz de arrependimento": para cada estado da natureza (coluna), encontre o melhor resultado. Em seguida, para cada célula daquela coluna, calcule a diferença entre o melhor resultado e o resultado da célula.
    2. Para cada alternativa (linha), identificar o valor máximo de arrependimento.
    3. Escolher a alternativa que possui o menor desses arrependimentos máximos.