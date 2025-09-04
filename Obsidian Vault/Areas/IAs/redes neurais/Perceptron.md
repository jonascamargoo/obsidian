O Perceptron é um algoritmo de classificação universal de dados (ou aproximador universal de funções) que decide se uma entrada pertence a uma de duas categorias. Ele faz isso multiplicando os dados de entrada por pesos e somando o resultado. Se essa soma ultrapassar um certo limiar, a saída é 1; caso contrário, é 0.

A principal limitação do Perceptron é que ele só funciona para problemas **linearmente separáveis**.

![[Pasted image 20250702073859.png]]


### O que é "Linearmente Separável"?

Um conjunto de dados é linearmente separável se você pode desenhar uma **única linha reta** (chamada de fronteira de decisão) para separar completamente os pontos de duas classes diferentes.

**Exemplos Visuais:**

#### Problemas Linearmente Separáveis (AND e OR)

As portas lógicas AND e OR são exemplos de problemas que um Perceptron pode resolver. Como mostram os gráficos abaixo, é possível traçar uma única linha verde para separar os resultados `1` (círculos azuis) dos resultados `0` (quadrados vermelhos).

- **Porta AND:** O resultado só é `1` quando ambas as entradas são `1`. Uma linha reta pode isolar este ponto dos outros.
    
- **Porta OR:** O resultado é `1` se pelo menos uma das entradas for `1`. Uma linha reta também pode separar os resultados.
    

	![[Pasted image 20250702074023.png]]

#### Problema Não Linearmente Separável (XOR)

A porta lógica XOR (OU Exclusivo) é um problema que um Perceptron **não consegue** resolver. O resultado é `1` apenas quando as entradas são diferentes (`0` e `1`, ou `1` e `0`).

Como o gráfico abaixo demonstra, **é impossível desenhar uma única linha reta** para separar os círculos azuis dos quadrados vermelhos. Você precisaria de mais de uma linha, o que torna o problema não linearmente separável.

![[Pasted image 20250702074124.png]]

## Então como ele resolve?

Como o perceptron simples resolve apenas problemas linearmente separáveis, então ele realiza uma aproximação de uma função de reta descrita na forma $f(x)=ax+b$

![[Pasted image 20250702080408.png]]


Para um neurônio com múltiplas entradas, a função é uma soma ponderada das entradas mais um bias (f representa o potencial de ativação):

$f(x_1,x_2,...,x_n)=w_1∗x_1+...+w_n∗x_n+b$

Esta soma ponderada, que representa o potencial de ativação do neurônio, para n igual a 3, é calculada como:

![[Pasted image 20250702090929.png]]
onde cada neurônio tem seu u

Esse valor `u` é o resultado da soma ponderada. É ele que é enviado para a **função de ativação**, que fará a decisão final (`0` ou `1`, para a sigmoidal).

## Algoritmo de Treinamento do Perceptron (Regra Delta)

Este algoritmo descreve o processo iterativo para ajustar os pesos ($w$) de um neurônio Perceptron a fim de minimizar o erro de classificação.

---

### Passo 1: Inicialização

1.  **Inicialize os pesos ($w_i$) e o bias ($b$)**: Atribua valores aleatórios e pequenos para todos os pesos e para o bias.
2.  **Defina a Taxa de Aprendizagem ($\eta$)**: Escolha um valor pequeno para a taxa de aprendizagem, geralmente entre $0.01$ e $1.0$. No seu exemplo, $\eta = 0.3$.

---

### Passo 2: Treinamento

Execute os passos a seguir repetidamente, em um laço de repetição, até que uma condição de parada seja atingida (ex: um número máximo de épocas ou um erro mínimo).

> **Para cada par de treinamento ($x, y$) no conjunto de dados, faça:**
>
> 1.  **Calcular a Saída do Neurônio ($o$):**
>     Execute o vetor de entrada $x$ na rede para obter a saída prevista $o$.
>     $$ o = f\left(\sum_{i=1}^{n} w_i x_i + b\right) $$
>     Onde $f$ é a função de ativação.
>
> 2.  **Calcular a Mudança no Peso ($\Delta w_i$):**
>     Para cada peso $w_i$, calcule o valor do ajuste usando a Regra Delta. O ajuste é proporcional à taxa de aprendizagem ($\eta$), ao erro ($y - o$), e à entrada correspondente ($x_i$).
>     $$ \Delta w_i \leftarrow \eta \cdot (y - o) \cdot x_i $$
>
> 3.  **Atualizar o Peso ($w_i$):**
>     Some o ajuste calculado ($\Delta w_i$) ao peso atual para obter o novo valor do peso.
>     $$ w_i \leftarrow w_i + \Delta w_i $$
>     *(O mesmo cálculo é feito para o bias, tratando-o como um peso com entrada fixa $x_0 = 1$)*

---

## Exemplo - O objetivo é treinar um Perceptron para aproximar a função $f(x) = 2x - 1$.

# Treinamento do Perceptron: Aproximação da Equação

O objetivo é treinar um Perceptron para aproximar a função $f(x) = 2x - 1$.

**Dados de Treinamento:**
| x | y |
|:---:|:---:|
| 0 | -1 |
| 1 | 1 |
| 2 | 3 |
| 3 | 5 |

**Fórmulas Utilizadas:**
- Potencial de Ativação: $u = \sum_{i=0}^{n} w_i \cdot x_i$
- Regra Delta: $\Delta w_i \leftarrow \eta(y - o) x_i$
- Atualização de Pesos: $w_i \leftarrow w_i + \Delta w_i$

---
#### 1ª Época

**Pesos Iniciais:** $w_0 = 0, w_1 = 0$.

### Amostra 1: (x=0, y=-1)
- $u = 0.0, o = 0.0$
- $\epsilon = 1$
- $\Delta w_0 = -0.3$
- $\Delta w_1 = 0.0$
- **Novos Pesos:** $w_0 = -0.3, w_1 = 0$

#### Amostra 2: (x=1, y=1)
- $u = -0.3, o = -0.3$
- $\epsilon = 1.3$
- $\Delta w_0 = 0.39$
- $\Delta w_1 = 0.39$
- **Novos Pesos:** $w_0 = 0.09, w_1 = 0.39$

### Amostra 3: (x=2, y=3)
- $u = 0.87, o = 0.87$
- $\epsilon = 2.13$
- $\Delta w_0 = 0.639$
- $\Delta w_1 = 1.278$
- **Novos Pesos:** $w_0 = 0.729, w_1 = 1.668$

#### Amostra 4: (x=3, y=5)
- $u = 5.733, o = 5.733$
- $\epsilon = 0.733$
- $\Delta w_0 = -0.219$
- $\Delta w_1 = -0.659$
#### Fim da 1ª Época

- **Erro Total da Época ($\epsilon_T$):** 5.163

---
#### 2ª Época

**Pesos Iniciais (vindos da época anterior):** $w_0 = 0.509, w_1 = 1.008$.

#### Amostra 1: (x=0, y=-1)
- $u = 0.509, o = 0.509$
- $\epsilon = 1.509$
- $\Delta w_0 = -0.452$
- $\Delta w_1 = 0.0$
- **Novos Pesos:** $w_0 = 0.056, w_1 = 1.008$

#### Amostra 2: (x=1, y=1)
- $u = 1.064, o = 1.064$
- $\epsilon = 1.064$
- $\Delta w_0 = -0.019$
- $\Delta w_1 = 0.037$
- **Novos Pesos:** $w_0 = 0.037, w_1 = 0.988$

#### Amostra 3: (x=2, y=3)
- $u = 2.014, o = 2.014$
- $\epsilon = 0.985$
- $\Delta w_0 = 0.295$
- $\Delta w_1 = 0.591$
- **Novos Pesos:** $w_0 = 0.332, w_1 = 1.580$

#### Amostra 4: (x=3, y=5)
- $u = 5.072, o = 5.072$
- $\epsilon = 0.072$
- $\Delta w_0 = -0.021$
- $\Delta w_1 = -0.065$

#### Fim da 2ª Época

- **Erro Total da Época ($\epsilon_T$):** 2.631

### Descrição do Fluxo de Treinamento do Perceptron

O texto que você forneceu é um exemplo prático e detalhado de como um neurônio Perceptron **aprende** de forma iterativa. O objetivo final é ajustar seus pesos internos para que ele consiga imitar a função matemática f(x)=2x−1.

O fluxo de treinamento pode ser entendido da seguinte forma:

#### 1. Preparação e Início (Pré-Treinamento)

O processo começa com a definição dos parâmetros básicos:

- **Modelo:** Um único neurônio com dois pesos: `$w_1$` (que aprenderá o coeficiente `2` da função) e `$w_0$` (o bias, que aprenderá o intercepto `-1`).
    
- **Dados:** Um conjunto de 4 amostras `(x, y)` que servem como "gabarito" para o treinamento.
    
- **Estado Inicial:** Na **1ª Época**, o Perceptron começa "sem conhecimento", com seus pesos inicializados em zero (`$w_0 = 0, w_1 = 0$`).
    

#### 2. O Processo Dentro de uma Época

Uma **época** consiste em apresentar ao Perceptron todo o conjunto de dados, amostra por amostra, de forma sequencial.

- **Para a primeira amostra `(x=0, y=-1)`:**
    
    1. O Perceptron calcula o **potencial de ativação `u`** (a soma ponderada), que resulta em `0.0`.
        
    2. Ele compara sua saída (`o=0.0`) com a saída esperada (`y=-1`) e calcula um **erro (`ε`)**.
        
    3. Usando a **Regra Delta (`Δw`)**, ele calcula o quanto precisa ajustar cada peso. Note que `Δw_1` é zero porque a entrada `x` era zero, então esse peso não teve contribuição para o erro.
        
    4. Finalmente, ele **atualiza seus pesos**.
        
- **Para as amostras seguintes (2, 3 e 4):** O ponto crucial do aprendizado é que para a segunda amostra, o Perceptron **não usa mais os pesos iniciais**, mas sim os pesos que acabaram de ser ajustados no passo anterior. Esse ciclo de **previsão -> cálculo de erro -> ajuste** se repete para cada amostra. A cada passo, os pesos são refinados, aproximando-se um pouco mais da solução ideal.
    

#### 3. A Transição Entre Épocas

- **Fim da 1ª Época:** Após o Perceptron ter visto todas as quatro amostras, a primeira época termina. O erro total (`$\epsilon_T$`) é de `5.163`, uma medida de quão "errado" o modelo estava nesse primeiro ciclo completo. Os pesos finais guardam todo o aprendizado adquirido.
    
- **Início da 2ª Época:** A segunda época não começa do zero. Ela parte dos **pesos finais da época anterior**. O Perceptron reinicia o processo, passando por todas as quatro amostras novamente, mas agora com um ponto de partida muito melhor.
    

#### 4. A Evidência do Aprendizado

O sucesso do treinamento é visível ao comparar o final das duas épocas:

- O erro total da 2ª Época (`2.631`) é quase a metade do erro da 1ª Época (`5.163`).
    

Isso demonstra que o fluxo está funcionando: a cada passagem completa pelos dados (a cada época), o Perceptron se torna progressivamente mais preciso em suas previsões, e seus pesos convergem lentamente para os valores ideais ($w_1 \approx 2$ e $w_0 \approx -1$). Este ciclo se repetiria por centenas ou milhares de épocas até que o erro se torne minimamente pequeno.