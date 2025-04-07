
## 🧠 O que é Programação Linear?

É uma técnica matemática usada para **otimizar** alguma coisa (como tempo, custo, lucro), considerando:

- Uma **função objetivo** (que você quer maximizar ou minimizar)
- Um conjunto de **restrições lineares** (limites do mundo real)
- Variáveis de decisão, que podem variar dentro dessas restrições


## 🧩 Como funciona?

### 1. **Variáveis de decisão**

São as incógnitas que queremos encontrar.

> **Exemplo (IA/ML):**  
> Quantas GPUs da AWS e quantos clusters locais usar para treinar um modelo de IA em 7 dias, minimizando o custo?

---

### 2. **Função objetivo**

É o que você quer otimizar. Pode ser custo, tempo, precisão, etc.

> **Exemplo (IA/ML):**  
> Minimize `Custo_total = 2x + 5y`, onde:
> 
> - `x` = horas em cluster local (R$2/h)
>     
> - `y` = horas na AWS (R$5/h)
>     

---

### 3. **Restrições lineares**

São limites do problema, como tempo disponível ou capacidade dos recursos.

> **Exemplo (IA/ML):**
> 
> - `x + y >= 168` (mínimo de horas pra treinar em 7 dias)
>     
> - `x <= 100` (limite do cluster local)
>     
> - `x, y >= 0` (não dá pra usar horas negativas)
>     

---

### 4. **Solução ótima**

Você usa técnicas (como o método Simplex ou solvers) para encontrar o melhor `x` e `y` que **minimizam o custo** e **respeitam as restrições**. Algumas bibliotecas em python utilizam programação linear por baixo dos panos, como o TensorFlow e Scikit-Lean


## 🧮 Exemplo resolvido com `PuLP` (em IA)


```python
from pulp import *

# Problema: minimizar custo de treino
prob = LpProblem("Treinamento_Modelo_IA", LpMinimize)

# Variáveis
x = LpVariable("Horas_Cluster_Local", lowBound=0)
y = LpVariable("Horas_AWS", lowBound=0)

# Função objetivo
prob += 2 * x + 5 * y, "Custo_Total"

# Restrições
prob += x + y >= 168
prob += x <= 100

# Resolver
prob.solve()

# Resultado
print(f"Local: {x.varValue}h, AWS: {y.varValue}h")

```

## Modelo de Problema de PL

1. Identificar as variáveis de decisão e representar através de símbolos algébricos (por exemplo, x e y ou x1 e x2)
2. Identifique o objetivo do problema. O objetivo de um problema de PL sempre será ou de maximizar
3. Descreva uma função linear com as variáveis de decisão que represente o problema apresentado. Essa função é a função objetivo de seu problema
4. Liste todas as restrições do problema e expresse-as como equações ou inequações em termos das variáveis de decisão definidas no passo anterior.

### Exemplo de um problema de programação linear

Uma empresa fabrica dois produtos 1 e produto 2. Na fabricação do produto 1 a empresa gasta nove horas-homem e três horas-máquina, onde a tecnologia utilizada é intensiva em mão-de-obra. Na fabricação do produto 2 a empresa gasta uma hora-homem e uma hora-máquina, onde a tecnologia é intensiva em capital. Sabendo-se que a empresa dispõe de 18 horas-homem e 12 horas-máquina e ainda que os lucros dos produtos são $4 e $1 respectivamente, quanto deve fabricar cada produto para obter o maior lucro possível ?

1. Passo: x1 e x2 as quantidades fabricadas dos produtos 1 e 2
2. Passo: maior lucro -> maximização
3. passo: a função lucro a ser maximizada é L = 4x1 + x2
4. passo: as quantidades fabricadas e as horas utilizadas de cada recurso não podem ultrapassar as quantidades de recursos disponíveis, logo, podemos deduzir as seguintes restrições:
	1. Para horas-homem: 9x1 + x2 <= 18
	2. Para horas-máquina: 3x1 + x2 <= 12
	3. Para não negatividade: x1, x2 >0
