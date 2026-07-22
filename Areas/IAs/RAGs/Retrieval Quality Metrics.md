---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-11-02'
---

Embora métricas de engenharia de software (latência, _throughput_, uso de recursos) sejam importantes, a métrica fundamental de um retriever é sua **qualidade de busca**.

Para "dar uma nota" a um retriever, três componentes são necessários:

1. O **Prompt** da consulta.
    
2. A **lista classificada (ranqueada)** de documentos que o retriever retorna.
    
3. Uma **lista de "ground truth"** (verdade absoluta) — o conjunto de todos os documentos _corretos_ (relevantes) na base de conhecimento para aquele prompt.
    

O principal gargalo de toda avaliação é o **custo da criação do _ground truth_**, que é um processo de anotação manual e demorado.

---

### Métricas Fundamentais: Precision e Recall

A avaliação de retriever é um problema clássico de Information Retrieval. As duas métricas de base são **Precision** (Precisão) e **Recall** (Revocação).

#### 1. Precision (Precisão)

- **O que mede:** A confiabilidade ou "pureza" dos resultados retornados. Penaliza o retriever por incluir documentos irrelevantes.
    
- **Fórmula:**
    
    $$ \text{Precision} = \frac{\text{Documentos Relevantes Recuperados}}{\text{Total de Documentos Recuperados}}$$
    
- **Exemplo:** Você recupera 12 documentos, dos quais 8 são relevantes. Sua precisão é $8/12 \approx 66.7\%$.
    

#### 2. Recall (Revocação)

- **O que mede:** A abrangência ou "completude" dos resultados. Penaliza o retriever por _deixar de encontrar_ documentos relevantes.
    
- **Fórmula:**
    
    $$ \text{Recall} = \frac{\text{Documentos Relevantes Recuperados}}{\text{Total de Documentos Relevantes (no Ground Truth)}}$$
    
- **Exemplo:** Havia 10 documentos relevantes no total. Você encontrou 8. Seu recall é $8/10 = 80\%$.
    

#### A Padronização: Métricas @K

Precision e Recall são inúteis sem um contexto. Se você aumentar o recall para $100\%$ (recuperando _todos_ os documentos da base), sua precisão será quase zero.

Por isso, as métricas são padronizadas em relação ao **Top K** (os `K` primeiros documentos retornados).

- **Precision@K:** Qual a precisão nos `K` primeiros resultados? (Ex: `Precision@5 = 40%` significa que 2 dos 5 primeiros eram relevantes).
    
- **Recall@K:** Qual o recall nos `K` primeiros resultados?
    

### Definindo as variáveis corretamente
### 1. Total de Documentos Relevantes (no Ground Truth)

- **O que é:** É o seu **Gabarito**. É o número total de documentos "corretos" que existem em _toda_ a sua base de conhecimento para aquela pergunta.
    
- **Como você sabe:** Este número é fixo e é determinado por um humano (você) _antes_ de avaliar a busca. Você teria que ler todos os 1.000 documentos e marcar: "Este fala de bônus, este também, este não...".
    
- **No Exemplo:** Você faz esse trabalho manual e descobre que, dos 1.000 documentos, existem **10** que respondem corretamente à pergunta.
    
    - **Total de Documentos Relevantes = 10**
        

### 2. Total de Documentos Recuperados

- **O que é:** É o número total de documentos que o seu retriever retornou. É simplesmente o tamanho da sua lista de resultados, ou seja, o valor de `K` que você pediu.
    
- **Como você sabe:** É o `K` que você definiu na sua busca (ex: `k=25` no seu código, ou `k=12` neste exemplo).
    
- **No Exemplo:** Você pediu os 12 melhores resultados.
    
    - **Total de Documentos Recuperados = 12**
        

### 3. Documentos Relevantes Recuperados

- **O que é:** É o número de **acertos** na sua lista de resultados. É a interseção dos dois grupos anteriores.
    
- **Como você sabe:** Você pega os 12 documentos que o retriever retornou (Grupo 2) e os compara com o seu gabarito de 10 documentos corretos (Grupo 1).
    
- **No Exemplo:** Dos 12 documentos que o retriever trouxe, você checa um por um e descobre que **8** deles realmente estavam na sua lista de 10 "corretos". Os outros 4 eram irrelevantes (ex: falavam de "férias").
    
    - **Documentos Relevantes Recuperados = 8**

---

### Métricas Sensíveis ao Rank (Rank-Aware)

`Precision@K` e `Recall@K` não se importam se o documento relevante está em 1º ou 10º lugar (desde que esteja no Top 10). Para medir a _qualidade do ranqueamento_, usamos métricas mais avançadas.

#### 1. Mean Average Precision (MAP) @ K

- **O que mede:** A qualidade média do ranqueamento. Recompensa _fortemente_ por colocar documentos relevantes nas primeiras posições.
    
- **Processo (para uma consulta - Average Precision):**
    
    1. Itere de `k=1` até `K`.
        
    2. Calcule a `Precision@k`.
        
    3. Some os valores de `Precision@k` **apenas para os ranks `k` onde o documento era relevante**.
        
    4. Divida essa soma pelo **número total de documentos relevantes encontrados** no Top K.
        
- **Exemplo (AP@5):**
    
    - Ranking: `[R, I, I, R, R]` (R=Relevante, I=Irrelevante)
        
    - `P@1` (R): $1/1 = 1.0$
        
    - `P@2` (I): $1/2 = 0.5$
        
    - `P@3` (I): $1/3 \approx 0.33$
        
    - `P@4` (R): $2/4 = 0.5$
        
    - `P@5` (R): $3/5 = 0.6$
        
    - Soma das precisões nos ranks relevantes (1, 4, 5): $1.0 + 0.5 + 0.6 = 2.1$
        
    - Total de relevantes encontrados: 3
        
    - **Average Precision (AP@5) = $2.1 / 3 = 0.7$**
        
- O **Mean Average Precision (MAP)** é simplesmente a média dos scores de `AP` de _múltiplas consultas (prompts)_. Um `MAP` alto indica que, em média, os documentos relevantes estão no topo do ranking.
    

#### 2. Mean Reciprocal Rank (MRR)

- **O que mede:** A rapidez com que o _primeiro_ documento relevante é encontrado. É uma métrica especializada, útil para tarefas onde "apenas uma resposta correta" é necessária (ex: perguntas de fato).
    
- **Processo (para uma consulta - Reciprocal Rank):**
    
    - Encontre o rank ($rank_1$) do **primeiro** documento relevante.
        
    - O score é o recíproco desse rank: $RR = 1 / rank_1$.
        
- **Exemplo:**
    
    - Se o primeiro doc relevante está em 1º: $RR = 1/1 = 1.0$
        
    - Se o primeiro doc relevante está em 4º: $RR = 1/4 = 0.25$
        
- O **Mean Reciprocal Rank (MRR)** é a média dos scores de `RR` de _múltiplas consultas_.
    

---

### Estratégia de Avaliação

A escolha da métrica depende do seu objetivo:

- **Recall@K** é a mais fundamental: O retriever está _encontrando_ os documentos necessários?
    
- **Precision@K** e **MAP@K** medem a _eficiência_: O retriever está poluindo os resultados com lixo? Os itens bons estão no topo?
    
- **MRR** é para _velocidade_: Com que rapidez o usuário vê o primeiro resultado útil?
    

Essas métricas são a única maneira de ajustar objetivamente os hiperparâmetros de um sistema de busca híbrida (ex: o peso entre busca semântica e keyword) e validar se as mudanças estão, de fato, melhorando o sistema.