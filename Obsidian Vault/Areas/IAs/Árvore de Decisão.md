
O algoritmo de Árvore de Decisão se destaca por sua simplicidade, interpretabilidade e poder preditivo. Utilizado tanto para tarefas de classificação quanto de regressão, este método simula o processo de tomada de decisão humano em uma estrutura intuitiva de árvore, tornando-o uma ferramenta valiosa para cientistas de dados e entusiastas da área.

### O que é uma Árvore de Decisão?

Em sua essência, uma Árvore de Decisão é um modelo de aprendizado supervisionado que utiliza uma estrutura de fluxograma em forma de árvore para tomar decisões. Ela é composta por:

- **Nós de Decisão (ou Nós Internos):** Representam um teste em um atributo (uma "pergunta").
    
- **Ramos:** Indicam o resultado do teste em um nó de decisão.
    
- **Nós Folha (ou Nós Terminais):** Representam um resultado final (uma classificação ou um valor).
    

O processo se inicia no **nó raiz**, que engloba todo o conjunto de dados. A partir dele, o algoritmo seleciona o melhor atributo para dividir os dados em subconjuntos mais homogêneos, criando novos nós de decisão e ramos. Esse processo de divisão continua recursivamente até que um critério de parada seja atingido, como a profundidade máxima da árvore ou a impossibilidade de novas divisões que melhorem o modelo.

### A Busca pela Pureza: O Coração da Árvore de Decisão

O objetivo principal de uma Árvore de Decisão é criar nós folha que sejam os mais "puros" possíveis. Em um contexto de classificação, um nó é considerado puro se todas as amostras de dados pertencentes a ele são da mesma classe. Para medir a impureza de um nó e, consequentemente, decidir qual atributo resultará na melhor divisão, são utilizadas métricas como:

- **Índice de Gini:** Mede a probabilidade de um elemento ser classificado incorretamente se fosse rotulado aleatoriamente de acordo com a distribuição das classes no nó. Um valor de Gini igual a 0 indica pureza total.
    
- **Entropia e Ganho de Informação:** A entropia mede o grau de desordem ou incerteza em um nó. O Ganho de Informação calcula a redução na entropia após a divisão de um nó por um determinado atributo. O algoritmo busca a divisão que maximize o ganho de informação.
    

A cada divisão, o algoritmo escolhe o atributo que resulta nos subconjuntos com a menor impureza (ou maior pureza), construindo assim uma árvore que segmenta os dados de forma cada vez mais específica.

#### Índice de Gini: a fórmula e a intuição

A fórmula do Gini é:

$$\text{Gini} = 1 - \sum_{k} p_k^2$$

Onde $p_k$ é a fração de amostras da classe $k$ no nó.

**Intuição:** o Gini responde à pergunta *"se eu pegasse uma amostra aleatória desse nó e tentasse adivinhar a classe baseado na distribuição, qual a probabilidade de errar?"*

- Nó **puro** (todos da mesma classe) → probabilidade de errar = 0 → **Gini = 0**
- Nó **50/50** (problema binário) → probabilidade de errar ≈ 0,5 → **Gini = 0,5** (máximo)

**Exemplos calculados** (problema binário Maligno × Benigno):

| Nó | Composição | Cálculo | Gini |
|---|---|---|---|
| Z | 100 Maligno / 0 Benigno | $1 - (1^2 + 0^2)$ | **0,00** (puro) |
| Y | 90 Maligno / 10 Benigno | $1 - (0{,}9^2 + 0{,}1^2)$ | **0,18** |
| X | 80 Maligno / 20 Benigno | $1 - (0{,}8^2 + 0{,}2^2)$ | **0,32** |
| W | 40 Maligno / 40 Benigno | $1 - (0{,}5^2 + 0{,}5^2)$ | **0,50** (impureza máxima) |

> [!warning] Armadilha comum em prova
> O valor máximo de Gini em um problema **binário** é **0,5**, não 1. Em problemas com $K$ classes, o máximo é $1 - 1/K$. Quem afirma que o Gini é 1 num nó 50/50 está errado.

#### Como a árvore escolhe o melhor split

Em cada nó, a árvore testa **todos os splits possíveis** (todas as features × todos os thresholds) e escolhe o que **mais reduz a impureza** somando os subnós (ponderados pelo tamanho de cada subnó).

Exemplo conceitual: um nó com Gini = 0,5 pode ser dividido em:

```
Split A:                       Split B:
  Subnó 1: Gini = 0.4            Subnó 1: Gini = 0.1
  Subnó 2: Gini = 0.3            Subnó 2: Gini = 0.2
  Média ponderada: 0.35          Média ponderada: 0.15
```

A árvore escolhe o **Split B** porque reduziu mais a impureza (de 0,5 para 0,15). Esse comportamento é **guloso**: a árvore otimiza localmente em cada nó, sem garantia de ótimo global.

### O Dilema da Profundidade: Quando a Perfeição se Torna um Problema

A busca incessante pela pureza absoluta em todos os nós folha leva a um crescimento significativo na altura (ou profundidade) da árvore (árvore de decisão é um algoritmo exaustivo). Cada nova divisão, por mais que aumente a pureza em relação aos dados de treinamento, adiciona um novo nível de complexidade ao modelo. É neste ponto que surge um dos principais desafios das Árvores de Decisão: o **overfitting**, ou sobreajuste.

Quando uma árvore se torna excessivamente profunda, ela começa a "memorizar" os dados de treinamento, incluindo seus ruídos e particularidades. As regras criadas nos nós mais profundos se aplicam a um número cada vez menor de amostras, perdendo a capacidade de generalização para novos dados, nunca antes vistos pelo modelo. Em outras palavras, o modelo se torna um **sistema especialista** no conjunto de dados de treinamento, mas falha em prever resultados para dados do mundo real.

![[Pasted image 20250808225025.png]]Exemplo de nó (esquerda) menos puro

![[Pasted image 20250808225152.png]]
Exemplo com nós mais puros (nó esquerdo, na branch de Cor). Tem menos variedades de formatos, porém a chance de acertar é maior. Temos mais informações sobre o que é uma Weissibier do que uma Pilsen, já que temos dois possíveis formato delas.

Imagine uma árvore de decisão para aprovação de crédito. Uma árvore muito profunda poderia criar uma regra como: "SE o cliente tem entre 30 e 32 anos, é do sexo masculino, possui dois cartões de crédito E o nome de seu animal de estimação é 'Rex', ENTÃO o crédito é aprovado". Embora essa regra possa ser perfeitamente acurada para uma única instância nos dados de treinamento, ela é completamente inútil e não generalizável para a população em geral.

Essa perda de amostras em nós cada vez mais específicos torna o sistema frágil e pouco robusto. A alta variância do modelo faz com que pequenas alterações nos dados de treinamento possam resultar em uma árvore completamente diferente.

Para combater o overfitting, técnicas como a **poda (pruning)** são empregadas. A poda consiste em remover partes da árvore (ramos e nós) que fornecem pouco poder preditivo, resultando em um modelo mais simples e com melhor capacidade de generalização. Outra abordagem é limitar a profundidade máxima da árvore ou definir um número mínimo de amostras por nó folha.

#### Diagnóstico: overfitting × underfitting em árvores

O diagnóstico é feito comparando o desempenho no treino e na validação:

| Diagnóstico | Score Treino | Score Validação | Gap | Causa estrutural |
|---|---|---|---|---|
| **Overfitting** | Alto (ex: 1,00) | Baixo (ex: 0,74) | **Grande** (≥ 10–20 pp) | Modelo complexo demais — memorizou ruído |
| **Underfitting** | Baixo (ex: 0,61) | Baixo (ex: 0,60) | **Pequeno** | Modelo simples demais ou regularização rígida demais |
| **Bem calibrado** | Alto (ex: 0,90) | Alto (ex: 0,87) | Pequeno | Capacidade adequada |

**Exemplo de overfitting** (Q18 do simulado): árvore com profundidade=18, 312 folhas, treino 100%, validação 74%. Diagnóstico: complexa demais. Ação: reduzir `max_depth`, aumentar `min_samples_leaf`, aplicar poda.

**Exemplo de underfitting** (Q22 do simulado): árvore com `max_depth=2`, `min_samples_leaf=200` num dataset de 1200 amostras, treino 0,59 / validação 0,58 em problema balanceado. Diagnóstico: restrições rígidas demais (cada folha precisa ter ≥17% do dataset!). Ação: relaxar as restrições.

> [!tip] Armadilhas frequentes
> - "Gap grande é normal" → **falso**. Gaps grandes sempre indicam overfitting.
> - "Mais dados sempre resolve overfitting" → **falso**. Se o modelo é estruturalmente livre, ele memoriza mais dados. Tem que **também** regularizar.
> - "Trocar `gini` por `entropy` corrige overfitting" → **falso**. Critérios geram árvores parecidas; quem regulariza são `max_depth`, `min_samples_leaf` e `ccp_alpha`.

### Hiperparâmetros de Regularização

A regularização é o conjunto de técnicas para limitar a complexidade da árvore e evitar overfitting. Os principais hiperparâmetros do `DecisionTreeClassifier`:

| Hiperparâmetro | O que controla | Aumentar → | Diminuir → |
|---|---|---|---|
| `max_depth` | Profundidade máxima da árvore | Mais complexidade, risco de overfitting | Mais simples, risco de underfitting |
| `min_samples_split` | Mínimo de amostras para dividir um nó | Árvore menor, mais regularizada | Árvore maior, mais splits possíveis |
| `min_samples_leaf` | Mínimo de amostras por folha | Folhas maiores, mais estabilidade | Folhas menores, mais overfitting possível |
| `ccp_alpha` | Penalidade por complexidade (poda) | Mais poda, árvore menor | Menos poda, árvore maior |
| `criterion` | Medida de impureza | `gini` (padrão, rápido) ou `entropy` |
| `class_weight` | Peso das classes | `'balanced'` corrige desbalanceamento; `None` é o padrão |

#### `class_weight='balanced'`: pesos, não amostras

> [!warning] Conceito crítico
> `class_weight='balanced'` **não altera o dataset**. Ele ajusta os **pesos** das classes inversamente proporcional à sua frequência, fazendo com que erros na classe minoritária sejam mais penalizados no cálculo de impureza.

Em um dataset com 950 negativos e 50 positivos:
- Sem `class_weight`: erro em positivo e negativo "valem" o mesmo. A árvore tende a ignorar a minoritária.
- Com `class_weight='balanced'`: erro em positivo "vale" ~19× mais (proporção 950/50). A árvore se esforça mais pra acertar positivos.

**Não confundir** com técnicas de resampling (que mudam o dataset):
- *Oversampling* (ex: SMOTE) → cria amostras sintéticas da minoritária
- *Undersampling* → remove amostras da majoritária
- `class_weight` → mantém o dataset, mas muda o cálculo interno

> [!info] Importante
> Mesmo usando `class_weight='balanced'`, **acurácia continua enganosa** em dados desbalanceados. Continue avaliando com F1, recall ou precision conforme o contexto.

### Cost-Complexity Pruning (`ccp_alpha`)

Uma das principais formas de regularização. A ideia é combinar erro e complexidade num único custo:

$$\text{Custo}(T) = \text{Erro}(T) + \alpha \times |T|$$

Onde $|T|$ é o número de folhas e $\alpha$ é a penalidade por complexidade.

**Intuição (analogia: comprando galhos):** cada folha "custa" $\alpha$, mas dá um "desconto" proporcional à redução de erro que ela traz.
- $\alpha$ baixo → galhos baratos → árvore grande
- $\alpha$ alto → galhos caros → só vale a pena ramos com grande retorno → árvore enxuta

| `ccp_alpha` | Efeito |
|---|---|
| 0 | Sem poda (árvore livre) |
| 0,0001 | Poda mínima (quase nada) |
| 0,01 | Poda moderada |
| 0,1 | Poda agressiva (árvore pode virar uma "tora") |

#### Procedimento correto para escolher `ccp_alpha`

> [!example] Método metodologicamente correto
> 1. Treinar a árvore **sem restrições** no conjunto de treino
> 2. Chamar `cost_complexity_pruning_path()` para obter a sequência de alphas candidatos
> 3. Para cada alpha candidato, treinar uma árvore podada com aquele alpha
> 4. Avaliar cada uma com **validação cruzada**
> 5. Escolher o alpha que dá o melhor score na validação
> 6. Treinar a árvore final usando esse melhor alpha

> [!fail] Erros comuns
> - "Calcular o caminho de poda no conjunto de teste" → **viola a regra de ouro** (teste é visto uma única vez no final)
> - "Escolher o maior alpha" → não faz sentido; maior alpha = poda mais agressiva = pode causar underfitting
> - "Usar `ccp_alpha=0.01` como padrão universal" → não existe valor universal; depende dos dados

### Vantagens e Desvantagens

| Vantagens | Desvantagens |
|---|---|
| Alta interpretabilidade — as regras podem ser lidas por humanos | Instável — pequenas mudanças nos dados podem mudar muito a estrutura da árvore |
| Não requer padronização ou normalização das features | Fronteira de decisão retangular — não captura relações diagonais sem muitas divisões |
| Lida com features numéricas e categóricas nativamente (em teoria; na prática do sklearn, precisa de encoding) | Tendência ao overfitting caso não seja regularizada |
| Rápida para treinar e prever | Viés em classes desequilibradas — tende a favorecer a classe majoritária |

### Pré-processamento: o que é obrigatório?

A árvore tem uma vantagem prática enorme: ela é **invariante a transformações monotônicas** e **só compara**, não calcula distância. Isso muda completamente o pré-processamento exigido em relação a outros algoritmos (como o [[KNN - Algoritmo de Classificação|KNN]]).

| Etapa | Obrigatória para árvore (sklearn)? | Por quê |
|---|---|---|
| Padronização (`StandardScaler`) | ❌ Opcional | A árvore só compara `feature ≤ threshold`. Escala não importa. |
| Log-transform (corrigir assimetria) | ❌ Opcional | Invariante a transformações monotônicas — log apenas muda o número do threshold, não a estrutura. |
| Encoding ordinal (categórica com ordem) | ✅ Obrigatória | `sklearn` não aceita strings; usar `OrdinalEncoder` preservando a ordem |
| Encoding one-hot (categórica nominal) | ✅ Obrigatória | `sklearn` não aceita strings; `OneHotEncoder` evita criar ordem artificial |
| Imputação de valores faltantes | ✅ Obrigatória | `DecisionTreeClassifier` do sklearn não aceita `NaN` |

> [!tip] Comparação rápida com o KNN
> No KNN, padronização é **obrigatória** (porque ele usa distância) e a árvore é "tolerante" — uma das suas grandes vantagens práticas. Veja [[KNN - Algoritmo de Classificação]] para o contraste detalhado.

### Quando usar uma Árvore de Decisão?

- **Interpretabilidade é requisito** — o cliente/regulador precisa entender as regras de decisão
- **Dados mistos** (numéricos e categóricos) sem pré-processamento extenso
- **Problema não muito complexo**, onde regras hierárquicas (`SE-ENTÃO-SENÃO`) fazem sentido
- Como **baseline** rápido para comparar com modelos mais complexos

#### Caso prático: contexto regulatório (aprovação de crédito)

> [!example] Cenário típico
> Banco precisa explicar ao cliente em linguagem simples por que o crédito foi negado. Auditor regulatório precisa rastrear todas as regras de decisão automatizada.

Nesse caso, a configuração adequada **não é** a árvore mais acurada possível, mas a **mais legível**:

```python
DecisionTreeClassifier(
    max_depth=3,           # no máximo 2³ = 8 folhas → cabe em uma página
    min_samples_leaf=50,   # folhas robustas, baseadas em padrões reais
    ccp_alpha=0.01,        # poda real, remove ramos que não compensam
)
```

Resultado: árvore com regras tipo *"se renda > 5.000 E idade > 30 E sem dívida ativa → aprovar"*. **Interpretabilidade vem da simplicidade estrutural**, não da fidelidade aos dados de treino. Em contextos regulatórios, sacrifica-se um pouco de acurácia para ganhar explicabilidade auditável.

### Pipeline de aplicação

1. Carregar e inspecionar os dados pré-processados (EDA)
2. Divisão estratificada: treino (65%) / validação (15%) / teste (20%)
3. **Baseline:** árvore sem restrições — diagnosticar overfitting (treino=100%, val<treino)
4. Seleção de features: `SelectFromModel` com threshold adequado
5. Validação cruzada estratificada com um modelo razoável
6. `GridSearchCV` ou `RandomizedSearchCV` — otimizar F1 (não acurácia em dados desbalanceados)
7. Poda (`ccp_alpha`): `cost_complexity_pruning_path` → CV por alpha → modelo final
8. Comparar candidatos no conjunto de validação — escolher pelo F1
9. **Avaliação final no teste** — uma única vez — `classification_report` + matriz de confusão
10. Análise de erros e `feature_importances_` para interpretabilidade

## Exemplo de código

```python

# %%

# Carregamento dos dados

import pandas as pd


df = pd.read_excel("data/dados_frutas.xlsx")

df # pq o df solto aqui? -> Quando a última linha de uma célula é uma variável ou um objeto (sem estar dentro de um print()), o ambiente automaticamente "inspeciona" esse objeto e exibe sua representação visual mais rica como a saída da célula.

# %%

# Preparação dos Dados para o Modelo
  

from sklearn import tree #scikit-learn é a maior lib de ML em python - im importing its decicion tree and its classifier

  

arvore = tree.DecisionTreeClassifier(random_state=42) # Cria uma "instância" vazia de um modelo de Árvore de Decisão para classificação. random_state=42 é um parâmetro para garantir que, se o algoritmo precisar de alguma aleatoriedade, os resultados sejam sempre os mesmos toda vez que o código for rodado, garantindo a reprodutibilidade.

  

y = df['Fruta'] # Separação da nossa variável-alvo. y é o que queremos que o modelo aprenda a prever. Neste caso, é a coluna "Fruta" da nossa tabela

  

caracteristicas = ["Arredondada","Suculenta",'Vermelha','Doce'] # Separação da nossa variável-alvo. y é o que queremos que o modelo aprenda a prever. Neste caso, é a coluna "Fruta" da nossa tabela.

  

X = df[caracteristicas] # Separação das nossas variáveis preditoras (features). X representa os dados que o modelo usará para fazer a previsão. Aqui, estamos selecionando apenas as colunas com as características da fruta.

  

# Aqui X e Y devem ter o mesmo número de linhas, pois cada linha de X corresponde a uma linha de y. Ou seja, cada fruta tem suas características e seu nome associado.

X

  

# %%

# ISSO AQUI E MACHINE LEARNING!!!!

arvore.fit(X, y) # O método .fit() treina o modelo. Ele analisa os dados X (características) e y (nomes das frutas) e "aprende" as regras e padrões que conectam as características a cada tipo de fruta. Por exemplo, ele pode aprender que "se 'Vermelha' for 1 e 'Arredondada' for 1, a chance de ser uma Maçã é alta".

  

# %%

# Fazendo uma Previsão Simples

arvore.predict([[1,1,1,0]]) # Agora usamos o modelo treinado para fazer uma previsão. Estamos fornecendo um novo dado para o modelo: uma fruta que não é Arredondada (0), não é Suculenta (0), não é Vermelha (0) e não é Doce (0). O modelo usará as regras que aprendeu para classificar essa nova fruta.

  

# %%

  

import matplotlib.pyplot as plt

  

plt.figure(dpi=400, figsize=[4,4])

  

tree.plot_tree(arvore,

feature_names=caracteristicas,

class_names=arvore.classes_,

filled=True)


#%%

proba = arvore.predict_proba([[1,1,1,1]])[0]
pd.Series(proba, index=arvore.classes_)

```


![[Pasted image 20250810133628.png]]Representação da árvore de decisão gerada

### Exemplo com regularização e poda

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import cross_val_score
import numpy as np

# 1. Árvore livre (baseline para diagnosticar overfit)
arvore_livre = DecisionTreeClassifier(random_state=42)
arvore_livre.fit(X_train, y_train)
print(f"Treino: {arvore_livre.score(X_train, y_train):.3f}")
print(f"Validação: {arvore_livre.score(X_val, y_val):.3f}")
# Se gap grande → overfitting

# 2. Calcular caminho de poda
path = arvore_livre.cost_complexity_pruning_path(X_train, y_train)
ccp_alphas = path.ccp_alphas[:-1]  # exclui o último (árvore vira só raiz)

# 3. Avaliar cada alpha via CV
scores = []
for alpha in ccp_alphas:
    clf = DecisionTreeClassifier(random_state=42, ccp_alpha=alpha)
    cv_scores = cross_val_score(clf, X_train, y_train, cv=5, scoring='f1')
    scores.append(cv_scores.mean())

# 4. Escolher o melhor alpha
melhor_alpha = ccp_alphas[np.argmax(scores)]

# 5. Treinar modelo final
arvore_final = DecisionTreeClassifier(random_state=42, ccp_alpha=melhor_alpha)
arvore_final.fit(X_train, y_train)
```
