
O **K-Nearest Neighbors (KNN)** é um dos algoritmos mais intuitivos de aprendizado de máquina supervisionado. Apesar da simplicidade, ele apresenta características particulares (sensibilidade a escala, lentidão na predição, sensibilidade a features irrelevantes) que precisam ser entendidas a fundo para ser usado corretamente.

> [!info] Veja também
> Para entender como escalar o KNN em produção (busca vetorial / RAG / embeddings) com bilhões de vetores, veja [[ANN - Escalabilidade da Busca Vetorial]]. Lá são discutidos algoritmos como **NSW** e **HNSW**, que são a evolução do KNN para busca aproximada em larga escala.

### A Intuição do KNN: "me diz com quem andas"

O KNN se baseia numa ideia super humana: classificar um ponto novo olhando para os pontos mais parecidos com ele que já foram vistos antes.

Se você quer classificar uma pessoa nova como "torcedor do Flamengo" ou "torcedor do Vasco", e você sabe que as 5 pessoas mais parecidas com ela (mesma vizinhança, mesma idade, mesmos hábitos) são todas flamenguistas, você apostaria que ela também é flamenguista. É exatamente isso que o KNN faz, mas num **espaço matemático**.

### O algoritmo em 3 passos

Para classificar um ponto novo:

1. **Calcular a distância** do ponto novo até **todos** os pontos do conjunto de treino
2. **Pegar os K pontos mais próximos** (os "K vizinhos")
3. **Votação:** a classe predita é a **maioria** entre esses K vizinhos

Só isso. Não tem fase de "aprendizado" complicada.

### Aprendizado Preguiçoso (Lazy Learning)

O KNN é um exemplo clássico de **aprendizado preguiçoso (lazy)**, em oposição ao aprendizado **ávido (eager)** de algoritmos como Árvore de Decisão ou SVM.

**Analogia:** dois professores preparando uma aula:
- **Ávido (eager):** estuda tudo antes, prepara um resumo, e na hora da aula consulta o resumo
- **Preguiçoso (lazy):** não estuda nada antes; quando alguém pergunta algo, corre na biblioteca procurar a resposta

Durante o `fit()`, o KNN literalmente só **memoriza** os dados — em pseudocódigo:

```python
def fit(self, X_train, y_train):
    self.X = X_train      # guarda os dados
    self.y = y_train      # guarda os rótulos
    # ... pronto. Acabou.
```

Toda a "inteligência" acontece na hora da **predição**, quando ele calcula distâncias.

| Aspecto | Ávido (Eager) | Preguiçoso (Lazy) |
|---|---|---|
| Exemplo | [[Árvore de Decisão]], SVM | **KNN** |
| `fit()` (treino) | 🐌 Caro — constrói modelo explícito | ⚡ Quase grátis — só armazena dados |
| `predict()` (predição) | ⚡ Rápida — percorre o modelo | 🐌 Cara — calcula distâncias para todos os pontos |
| Memória após treino | Baixa — só o modelo | Alta — todo o treino fica em memória |

> [!tip] Sacada importante
> Lazy × eager é uma questão de **quando** o trabalho é feito, não de **quanto** trabalho total. Ávido faz tudo no treino; preguiçoso adia tudo para a predição.

> [!warning] Detalhe sobre kd-tree / ball-tree
> Algumas implementações do KNN constroem uma estrutura de indexação (`kd-tree`, `ball-tree`) no `fit()` para acelerar a busca de vizinhos. Isso **não muda** sua natureza preguiçosa — é só uma forma eficiente de organizar os dados para a busca posterior. A diferença é como organizar livros na estante por ordem alfabética (estrutura) vs ler e entender os livros (modelo explícito).

### Medidas de distância

A pergunta crucial do KNN é: o que significa "vizinho próximo"? Isso depende de qual **distância** você escolhe.

#### Família Minkowski

A fórmula geral:

$$d(a, b) = \left(\sum_i |a_i - b_i|^p\right)^{1/p}$$

Variando o $p$ obtemos diferentes distâncias:

| $p$ | Nome | Fórmula | Interpretação |
|---|---|---|---|
| 1 | **Manhattan** | $\sum_i \|a_i - b_i\|$ | Distância "em táxi" — soma das diferenças absolutas |
| 2 | **Euclidiana** | $\sqrt{\sum_i (a_i - b_i)^2}$ | Distância em linha reta (padrão do sklearn) |
| ∞ | **Chebyshev** | $\max_i \|a_i - b_i\|$ | Maior diferença em qualquer dimensão |

**Exemplo numérico** (Q24 do simulado): para A = (0, 0) e B = (3, 4):

- **Manhattan** = $|0-3| + |0-4| = 3 + 4 = \mathbf{7}$
- **Euclidiana** = $\sqrt{9 + 16} = \sqrt{25} = \mathbf{5}$
- **Chebyshev** = $\max(3, 4) = \mathbf{4}$

Visualização:

```
       B (3,4)
       •
      ╱│
     ╱ │
    ╱  │ 4
   ╱   │
  ╱    │
 •─────┘
 A     3
 (0,0)

Euclidiana (5): a hipotenusa — voa direto
Manhattan (7): cateto + cateto — anda pelos eixos
Chebyshev (4): só o maior cateto
```

> [!info] Propriedade matemática
> Sempre vale: **Chebyshev ≤ Euclidiana ≤ Manhattan**. Não é coincidência — decorre da definição da família Minkowski.

| Distância | Características | Quando preferir |
|---|---|---|
| **Euclidiana** ($p=2$) | Sensível a outliers (diferenças ao quadrado) | Dados contínuos, bem distribuídos, sem outliers extremos |
| **Manhattan** ($p=1$) | Mais robusta a outliers (cresce linearmente) | Dados com ruído ou outliers, alta dimensionalidade |
| **Chebyshev** ($p=\infty$) | Considera apenas a maior diferença | Quando uma variação grande em qualquer dimensão já decide (ex: xadrez, RPG) |

#### Distância de Mahalanobis

A Mahalanobis considera a **correlação entre features** e a variabilidade de cada uma. Calcula a distância tendo em conta a matriz de covariância, tornando-se ideal quando as features estão em **escalas muito diferentes** ou são **altamente correlacionadas**.

**Quando usar:**
- **Variáveis com correlação:** features que interagem entre si (peso e altura, ou área e número de quartos). A Euclidiana assume independência; Mahalanobis captura o efeito conjunto.
- **Escalas distintas:** se as variáveis estão em unidades muito diferentes e você quer evitar padronizar manualmente
- **Detecção de outliers:** Mahalanobis indica a quantos desvios-padrão um ponto está do centro dos dados — excelente para detecção de fraudes
- **Grupos em formato de elipse:** quando as classes estão espalhadas em formatos esticados (elípticos) em vez de agrupamentos redondos

#### Jaccard e SMC (dados binários)

Para dados **binários** (presença/ausência), existem medidas específicas:

| Medida | Fórmula | Diferença chave |
|---|---|---|
| **Jaccard** | $\frac{\|A \cap B\|}{\|A \cup B\|}$ | **Ignora** as co-ausências (0-0) |
| **SMC** (Simple Matching Coefficient) | $\frac{\text{iguais 0-0} + \text{iguais 1-1}}{\text{total}}$ | **Inclui** as co-ausências (0-0) |

**Quando usar cada uma:**

> [!example] Jaccard — texto e recomendação
> Imagine dois usuários de streaming, cada um indicando quais de 1000 filmes assistiram. Usuário A viu 5 filmes, B viu 4 (3 em comum). Eles também "não viram" 993 filmes em comum — mas isso **não os torna similares**, porque quase ninguém viu a maioria dos filmes. Jaccard ignora essas co-ausências, focando só no que eles assistiram juntos.

> [!example] SMC — sintomas clínicos
> Dois pacientes com lista de 50 sintomas. A tem 3 sintomas, B tem 4 (3 em comum). Eles também não têm 44 sintomas em comum — e isso **é clinicamente relevante**: "não ter febre", "não ter dor de cabeça" são observações médicas reais. SMC conta essas concordâncias 0-0 como similaridade.

| Medida | Conta 1-1? | Conta 0-0? | Use quando... |
|---|---|---|---|
| **Jaccard** | ✅ | ❌ | Ausência é ruído (texto, recomendação) |
| **SMC** | ✅ | ✅ | Ausência é informativa (clínico, presença de atributos) |

### Padronização é Obrigatória no KNN

Esta é a regra **mais importante** ao usar KNN. Features em escalas diferentes fazem com que a feature de maior magnitude **domine completamente** o cálculo de distância.

> [!example] Exemplo concreto do problema de escala
> Cliente A: idade=25, salário=R$ 3.000  
> Cliente B: idade=30, salário=R$ 5.000  
> Cliente C: idade=45, salário=R$ 50.000  
>
> Distância euclidiana A↔B sem padronizar:  
> $\sqrt{(25-30)^2 + (3000-5000)^2} = \sqrt{25 + 4.000.000} \approx 2000$  
>
> A diferença de **idade** (25) é completamente engolida pela diferença de **salário** (4.000.000). A idade vira **irrelevante** no cálculo, mesmo sendo uma feature importante.

A solução é padronizar **após** a divisão dos dados (treino/validação/teste):

#### StandardScaler vs MinMaxScaler

Existem duas formas comuns de padronizar:

**StandardScaler** — Z-score:

$$z = \frac{x - \mu}{\sigma}$$

Resultado: feature com média 0 e desvio padrão 1. Valores tipicamente entre -3 e +3.

**MinMaxScaler** — comprime para [0, 1]:

$$x_{novo} = \frac{x - x_{min}}{x_{max} - x_{min}}$$

Resultado: menor valor vira 0, maior vira 1, restante distribuído proporcionalmente.

| Aspecto | StandardScaler | MinMaxScaler |
|---|---|---|
| Faixa de saída | Variável (~[-3, +3]) | Fixa: [0, 1] |
| Centro | Sempre em 0 | Nenhum específico |
| Considera distribuição? | Sim (usa média e desvio) | Não (só usa min e max) |
| Sensível a outliers? | Menos 🛡️ | **Muito** 🚨 |

> [!warning] O calcanhar de Aquiles do MinMaxScaler
> Imagine salários entre R$ 3.000 e R$ 50.000, mas com um outlier de R$ 5.000.000 (um CEO):
>
> - Com MinMax: o salário de R$ 50.000 vira **0,009** — todos os salários "normais" ficam comprimidos perto de zero, e o outlier sozinho ocupa quase todo o espaço [0, 1].
> - Com Standard: o outlier vai pra algo como +50, mas os outros ficam bem distribuídos.

**Regra prática:** começar com `StandardScaler`. É mais robusto em dados reais. Use `MinMaxScaler` quando souber que os dados não têm outliers e a distribuição é uniforme.

> [!fail] Regra de ouro: NUNCA `fit()` no teste
> ```python
> # ✅ CORRETO
> scaler = StandardScaler()
> scaler.fit(X_train)                     # fit() APENAS no treino
> X_train_s = scaler.transform(X_train)
> X_test_s = scaler.transform(X_test)     # só transform no teste
>
> # ❌ ERRADO (vazamento de dados)
> X_train_s = scaler.fit_transform(X_train)
> X_test_s = scaler.fit_transform(X_test)  # NUNCA! reaprende com o teste
> ```
> Se você fizer `fit_transform` no teste, o scaler "espia" as estatísticas dos dados que deveriam simular "dados novos", e sua estimativa de desempenho fica otimista demais.

### O hiperparâmetro K: o coração do KNN

O `n_neighbors` (K) controla o trade-off **overfitting × underfitting**.

| K | Comportamento | Diagnóstico |
|---|---|---|
| **K=1** | Cada ponto manda na sua região | 🔥 **Overfitting puro** — memoriza ruído. 100% no treino. |
| **K médio (5-15)** | Equilíbrio entre detalhe e generalização | ✅ Geralmente o ideal |
| **K muito grande** | Quase tudo vira a classe majoritária | 🥶 **Underfitting** — perde nuance |

#### Por que K=1 é o "teto do overfitting"?

> [!example] A ilusão dos 100% no treino
> Com K=1, ao avaliar **no treino**, cada ponto encontra **ele mesmo** como vizinho mais próximo (distância zero). Copia a própria classe → acerta 100%, sempre.
>
> Esse 100% no treino é **artificial** — não significa que o modelo aprendeu, significa apenas que ele está "lembrando" de cada ponto. Na validação, ele falha porque qualquer ruído ou outlier nos dados de treino vira "lei" e cria pequenas bolhas de classe erradas.

Visualização da fronteira de decisão:

```
K=1 (overfit):                     K=15 (suave):
                                    
  □ □   ●                          □ □   ●
  □  ╲╱ ●        Bolhas pequenas   □       ●     Fronteira
  □  ╱╲ ●        contornando       □   ╲   ●     suave
  □    ●         cada ponto        □ □  ╲  ●     
                                                 
```

> [!warning] Não pular direto para K muito grande
> Se K=1 está em overfitting, a tentação é pular para K=50. **Não faça isso sem validação.** K muito grande causa underfitting (o modelo praticamente prevê a classe majoritária sempre). O correto é encontrar o K ótimo via **validação cruzada**, plotando F1 × K.

```
F1
1.0 ┤
0.9 ┤        ╭───╮                  
0.8 ┤      ╭─╯   ╰╮                 
0.7 ┤ ╭───╯       ╰──╮              
0.6 ┤─╯              ╰────╮         
0.5 ┤                      ╰─────── 
    └────────────────────────────────
     1   5   9   13   17   21   25  k
     ↑       ↑                    ↑
   overfit  ótimo              underfit
```

### Hiperparâmetros do KNN

| Hiperparâmetro | Efeito | Observação |
|---|---|---|
| `n_neighbors` (K) | Regularização. K pequeno = overfit; grande = underfit | Mais impactante; escolher por CV |
| `weights` | `'uniform'` (votos iguais) ou `'distance'` (vizinhos mais próximos pesam mais) | Útil em regiões de fronteira |
| `metric` / `p` | Define a medida de distância | Euclidiana padrão; Mahalanobis para dados correlacionados |

#### Por que `GridSearchCV` em vez de `RandomizedSearchCV`?

O espaço de busca do KNN é pequeno e bem delimitado:
- `n_neighbors`: 1 a 30 → 30 valores
- `weights`: `['uniform', 'distance']` → 2 valores
- `p`: `[1, 2]` → 2 valores

Total: $30 \times 2 \times 2 = 120$ combinações. Cobertura total é viável; não há motivo para amostrar aleatoriamente.

### Maldição da Dimensionalidade e Features Irrelevantes

O KNN é **especialmente sensível** a:

1. **Features em escalas diferentes** → resolve com padronização
2. **Features irrelevantes** → resolve com seleção de features
3. **Alta dimensionalidade** → resolve com redução de dimensionalidade

> [!warning] Features irrelevantes contaminam a distância
> Imagine um dataset com 30 features, onde **20 são puro ruído**. Cada feature contribui com algum valor (ruidoso) no cálculo de distância:
>
> $$d = \sqrt{(f_1^A - f_1^B)^2 + \dots + (f_{30}^A - f_{30}^B)^2}$$
>
> Os 20 valores ruidosos vão estar somados junto com os 10 valores que **realmente importam**. O ruído pode dominar o sinal. Diferente de uma [[Árvore de Decisão]] (que escolhe as melhores features em cada split), o KNN **não tem mecanismo de seleção** — todas as features entram com peso igual.

A complexidade do KNN é $O(N \times d)$, onde $N$ é o número de amostras e $d$ é o número de features. Features irrelevantes aumentam $d$ — degradam **qualidade da predição** e tempo de processamento (linearmente em $d$, não quadraticamente).

### Vantagens e Desvantagens

| Vantagens | Desvantagens |
|---|---|
| Simples de implementar e entender | Lento na predição — $O(N \times d)$ por amostra |
| Não exige suposição sobre a distribuição dos dados | Altíssimo consumo de memória — armazena todo o treino |
| Fronteira de decisão adaptativa (não-linear) | Sensível à escala — padronização **obrigatória** |
| Poucos hiperparâmetros | Sensível a features irrelevantes |
| Fácil de atualizar (adicionar amostras de treino) | Degradação em alta dimensionalidade |

### Quando usar KNN?

**Use quando:**
- Dataset pequeno ou médio (predição lenta é tolerável)
- Fronteira de decisão não-linear complexa
- Interpretabilidade local é necessária (inspecionar os vizinhos que causaram a decisão)
- Sistemas de recomendação (similaridade entre usuários/itens)
- Detecção de anomalias baseada em densidade de vizinhos

**Evite quando:**
- Dataset gigante (predição vira gargalo) — nesse caso, considere [[ANN - Escalabilidade da Busca Vetorial|ANN/HNSW]]
- Muitas features irrelevantes sem seleção prévia
- Alta dimensionalidade sem redução

### Pipeline de aplicação

1. Carregar os dados e inspecionar escalas (`describe().T`)
2. **Divisão estratificada** treino / validação / teste — **antes** de padronizar
3. **Padronização:** `StandardScaler.fit()` apenas no treino, `transform()` em todos
4. Baseline: KNN k=1 (teto do overfitting) e k=5 (padrão)
5. `Pipeline(scaler + knn)` para garantir reaplicação do scaler dentro do CV
6. Validação cruzada estratificada com scoring adequado (F1 para desbalanceamento)
7. `GridSearchCV`: `n_neighbors` (1-30), `weights` (`'uniform'`, `'distance'`), `p` (1, 2)
8. Comparar candidatos no conjunto de validação
9. **Avaliação final no teste** — uma única vez
10. Análise de erros: `kneighbors()` para inspecionar vizinhos dos erros

### Exemplo de código completo

```python
from sklearn.neighbors import KNeighborsClassifier
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline
from sklearn.model_selection import GridSearchCV, train_test_split

# 1. Divisão estratificada (ANTES de padronizar!)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, stratify=y
)

# 2. Pipeline garantindo que o scaler seja reaplicado em cada fold do CV
pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('knn', KNeighborsClassifier())
])

# 3. GridSearch — note os prefixos 'knn__' (sintaxe obrigatória com Pipeline)
param_grid = {
    'knn__n_neighbors': range(1, 31),
    'knn__weights': ['uniform', 'distance'],
    'knn__p': [1, 2]  # 1 = Manhattan, 2 = Euclidiana
}

gs = GridSearchCV(pipe, param_grid, cv=5, scoring='f1')
gs.fit(X_train, y_train)

print(f"Melhores parâmetros: {gs.best_params_}")
print(f"Melhor F1 (CV): {gs.best_score_:.3f}")

# 4. Avaliação final no teste — UMA ÚNICA VEZ
f1_teste = gs.score(X_test, y_test)
print(f"F1 no teste: {f1_teste:.3f}")
```

> [!fail] Erros comuns no código de KNN
> 1. **Padronizar antes de dividir** → vazamento das estatísticas do teste para o scaler
> 2. **Scaler fora do Pipeline no CV** → vazamento entre folds
> 3. **Esquecer o prefixo `knn__`** no `param_grid` quando usar Pipeline → erro `"Invalid parameter X for estimator Pipeline"`
> 4. **`fit_transform` no teste** → reaprende as estatísticas; deve ser só `transform`
> 5. **KNN sem padronização** em features com escalas diferentes → uma feature domina tudo

### Pipeline de pré-processamento típico

Cenário com features mistas (numéricas, categóricas, faltantes):

| Tipo de feature | Etapa | Por quê |
|---|---|---|
| Numérica com NaN | **Imputação** (média/mediana) | KNN não aceita NaN no cálculo de distância |
| Categórica nominal | **OneHotEncoder** | KNN não aceita strings; OneHot evita criar ordem artificial |
| Categórica ordinal | **OrdinalEncoder** (preservando ordem) | Quando a ordem das categorias é informativa |
| Numérica | **StandardScaler** (após imputação e encoding) | Coloca todas as features na mesma escala |

> [!info] Ordem importa!
> A ordem correta é: **(1) Encoding** → **(2) Imputação** → **(3) Scaling** → **(4) KNN**. Tentar padronizar antes de codificar é impossível (não dá pra calcular média de strings); tentar padronizar antes de imputar quebra (NaN distorce ou impede o cálculo de média/desvio).

### Comparação rápida: KNN vs Árvore de Decisão

| Aspecto | KNN | [[Árvore de Decisão]] |
|---|---|---|
| Tipo de aprendizado | Preguiçoso (lazy) | Ávido (eager) |
| Treinamento | Quase grátis (memoriza) | Caro (busca de splits) |
| Predição | Cara (calcula distâncias) | Rápida (percorre árvore) |
| **Padronização** | **Obrigatória** | Não necessária |
| Fronteira de decisão | Suave, adaptativa | Retangular, paralela aos eixos |
| Interpretabilidade | Baixa (sem regras explícitas) | Alta (regras legíveis) |
| Overfitting | Com K=1 | Sem regularização |
| Regularização | `n_neighbors` (K) | `max_depth`, `min_samples_leaf`, `ccp_alpha` |
| Dados faltantes | Não tolera | Algumas implementações toleram |
| Alta dimensionalidade | Fortemente afetado (maldição) | Moderadamente afetado |
| Features irrelevantes | Contaminam a distância | Naturalmente ignoradas |
| Quando usar | Fronteira complexa, recomendação, anomalias | Interpretabilidade, dados mistos, baseline |
