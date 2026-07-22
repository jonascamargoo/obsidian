---
tipo: conceito
area: IAs
tags:
- ia/logica-fuzzy
criada: '2025-04-14'
---

## 🧠 Introdução à Lógica Fuzzy

A **Lógica Fuzzy**, ou **Lógica Nebulosa**, é uma extensão da lógica booleana tradicional. Enquanto a lógica booleana trabalha com apenas dois valores (0 e 1, ou falso e verdadeiro), a fuzzy permite que existam **valores intermediários**, como 0.3 ou 0.8, representando graus de verdade ou grau de pertencimento a um conjunto.

> 🔍 **Insight**: Isso é útil para modelar incertezas ou informações vagas do mundo real, como "está quente", "é alto", "está próximo".

- Lógica Clássica:
    
    - João tem 1,80 m → "É alto" = verdadeiro (1)
        
    - João tem 1,65 m → "É alto" = falso (0)
        
- Lógica Fuzzy:
    
    - João tem 1,80 m → "É alto" = 0.9
        
    - João tem 1,65 m → "É alto" = 0.4

## 🧩 Conjuntos Fuzzy

Na lógica clássica, um elemento pertence ou não a um conjunto. Já em conjuntos fuzzy, **existe um grau de pertencimento**, definido por uma **função de pertinência**.

Um conjunto fuzzy A~\tilde{A}A~ é definido como:

$$
\tilde{A} = \{(x, \mu_{\tilde{A}}(x)) \,|\, x \in X\}
$$

Se definirmos o conjunto fuzzy "temperaturas quentes", podemos ter:

- 25°C → µ = 0.3
    
- 30°C → µ = 0.7
    
- 35°C → µ = 1.0
    

> 🔍 **Insight**: Essa função μ\muμ (função de pertinência) varia de 0 a 1 e pode ter diversos formatos, como linear, triangular, trapezoidal ou gaussiana.


## 📈 Formas de Função de Pertinência

#### 1. **Triangular**:

Tem um formato de pirâmide e três parâmetros: a, b e c, onde:

- a: início da subida
- b: valor máximo (pertinência 1)
- c: fim da descida

$$
\mu(x) = 
\begin{cases}
0, & \text{se } x \leq a \text{ ou } x \geq c \\
\frac{x - a}{b - a}, & \text{se } a < x \leq b \\
\frac{c - x}{c - b}, & \text{se } b < x < c \\
\end{cases}
$$

       /\
      /  \
     /        \
------a-------b------c----

Para representar "temperatura agradável" com:

- a = 18
- b = 24
- c = 30

Você teria:

- 18°C → µ = 0
    
- 24°C → µ = 1
    
- 30°C → µ = 0

#### 2. **Trapezoidal**:

É como a triangular, mas com um platô no topo, ou seja, **tem uma faixa com pertinência máxima**.
- a,b: subida
- c,d: descida

       _______
      /       \
     /                 \
----a--b-----------c--d----

$$
\mu(x) = 
\begin{cases}
0, & \text{se } x \leq a \text{ ou } x \geq d \\
\frac{x - a}{b - a}, & \text{se } a < x \leq b \\
1, & \text{se } b < x \leq c \\
\frac{d - x}{d - c}, & \text{se } c < x < d \\
\end{cases}
$$


"Nota boa" entre 7 e 10:

- a = 6
- b = 7
- c = 9
- d = 10

Você teria pertinência 1 entre 7 e 9.
#### 3. **Gaussiana**
Representa uma curva suave (em forma de sino), com centro c e largura σ.

$$
\mu(x) = e^{-\frac{(x - c)^2}{2\sigma^2}}
$$


## 🔄 Operações Fuzzy

As principais operações em lógica fuzzy são generalizações das operações clássicas:

| Operação           | Lógica Clássica | Lógica Fuzzy |
| ------------------ | --------------- | ------------ |
| **E** (interseção) | min(a, b)       | min(a, b)    |
| **OU** (união)     | max(a, b)       | max(a, b)    |
| **NÃO**            | 1 - a           | 1 - a        |

> 🧠 Insight: Repare que a "E" fuzzy é o mínimo entre os valores, e a "OU" fuzzy é o máximo. Isso mantém a ideia intuitiva de interseção e união, mas agora com "intensidade".


![[Pasted image 20250406200019.png]]

![[Pasted image 20250406200549.png]]
![[Pasted image 20250406200830.png]]
![[Pasted image 20250406201544.png]]


## ⚙️ Sistema Fuzzy

Um sistema fuzzy típico é composto por:

1. **Fuzzificação**: transforma variáveis nítidas (crisp) em fuzzy (ex: de 32°C para µ_quente = 0.8).
    
2. **Inferência**: aplica as regras do tipo “SE ... ENTÃO ...”.
    
3. **Agregação**: combina os resultados das regras.
    
4. **Defuzzificação**: converte o valor fuzzy de volta para um valor nítido (ex: µ = 0.7 vira 31°C).

"SE temperatura é quente E umidade é baixa ENTÃO ventilador = alto"

![[Pasted image 20250406210536.png]]

#### Exemplo de Fuzzificação: Freio

Vamos considerar um sistema fuzzy para controle de um freio. O objetivo é ajustar a força de frenagem de forma inteligente, baseada em dois fatores principais: a **velocidade do veículo** e o **deslizamento das rodas**.

#### Entradas do sistema fuzzy

1. **Velocidade do veículo (km/h)**:  
    Representada linguisticamente como:
    - Baixa
    - Média
    - Alta
2. **Deslizamento das rodas (%)**:  
    Representada linguisticamente como:
    - Pequeno
    - Médio
    - Grande

### Saída do sistema fuzzy

- **Força de frenagem**:
    - Fraca
    - Moderada
    - Forte

### Fuzzificação de valores

Imagine que o veículo está a **85 km/h** com **30% de deslizamento** nas rodas.
##### Funções de pertinência

**Velocidade** (triangular):

- Baixa: 0 a 50 km/h
- Média: 40 a 100 km/h
- Alta: 80 a 150 km/h

**Deslizamento** (triangular):

- Pequeno: 0 a 20%
    
- Médio: 15 a 45%
    
- Grande: 40 a 100%

**Cálculo das pertinências**

$$
\textbf{Velocidade: } x = 85 \, \text{km/h}
$$

$$
\mu_{\text{média}}(85) = \frac{100 - 85}{100 - 70} = \frac{15}{30} = 0{,}5
$$

$$
\mu_{\text{alta}}(85) = \frac{85 - 80}{100 - 80} = \frac{5}{20} = 0{,}25
$$

---

$$
\textbf{Deslizamento: } x = 30\%
$$

$$
\mu_{\text{médio}}(30) = \frac{45 - 30}{45 - 15} = \frac{15}{30} = 0{,}5
$$

$$
\mu_{\text{grande}}(30) = 0
$$


### Regras fuzzy (exemplos)

1. Se a velocidade for **alta** e o deslizamento for **grande**, então a força de frenagem será **fraca**.
2. Se a velocidade for **média** e o deslizamento for **médio**, então a força de frenagem será **moderada**.
3. Se a velocidade for **baixa** e o deslizamento for **pequeno**, então a força de frenagem será **forte**.


OBS importantes: na hora de defuzzificar e achar o centro de massa do triângulo/trapézio (achando a desejabilidade), devemos analisar a função (quando o ponto em questão não é horizontal) para saber 