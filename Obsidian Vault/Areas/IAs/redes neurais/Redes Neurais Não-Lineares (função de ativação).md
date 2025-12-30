
Este módulo aborda as limitações fundamentais da regressão linear e introduz a arquitetura necessária para modelar sistemas complexos e não-lineares, como o tráfego urbano heterogêneo.

## 1. O Problema da Linearidade (The Linear Trap)

No laboratório anterior, observou-se que modelos lineares falham quando a complexidade do sistema aumenta (ex: introdução de carros e tráfego).

- **Fenômeno:** O modelo linear assume uma taxa de variação constante ($\frac{dy}{dx} = k$).
    
- **Realidade:** A relação entre distância e tempo varia dinamicamente (tráfego urbano denso vs. rodovias rápidas). O modelo linear sofre de **Underfitting** (subajuste) severo.


### A Falácia da Adição de Neurônios

Intuitivamente, poderíamos pensar em adicionar mais neurônios para capturar mais complexidade. No entanto, matematicamente, **empilhar transformações lineares resulta apenas em outra transformação linear.**

Seja um modelo com duas camadas lineares sem ativação:

1. Camada Oculta: $z = W_1 x + b_1$
    
2. Camada de Saída: $\hat{y} = W_2 z + b_2$
    

Substituindo (1) em (2):

$$\hat{y} = W_2(W_1 x + b_1) + b_2 \\ \hat{y} = (W_2 W_1) x + (W_2 b_1 + b_2)$$

Podemos redefinir $W' = W_2 W_1$ e $b' = W_2 b_1 + b_2$. Logo:

$$\hat{y} = W' x + b'$$

**Conclusão:** Sem uma função não-linear entre as camadas, a rede colapsa matematicamente em uma regressão linear simples, independentemente da profundidade.
![[Pasted image 20251217162240.png]]

---

## 2. A Solução: Funções de Ativação

Para que a rede neural aprenda curvas e padrões complexos, precisamos introduzir uma não-linearidade após cada transformação linear.
![[Pasted image 20251217162357.png]]
### ReLU (Rectified Linear Unit)

A função **ReLU** é o padrão da indústria ("workhorse") para Deep Learning moderno devido à sua eficiência computacional e capacidade de mitigar o problema do desaparecimento de gradiente (vanishing gradient).

**Definição Matemática:**

$$f(x) = \max(0, x) = \begin{cases} 0 & \text{se } x < 0 \\ x & \text{se } x \geq 0 \end{cases}$$

Interpretação Geométrica:

A ReLU introduz uma "dobra" (bend) ou articulação na função. Ela desativa o neurônio (saída 0) para valores negativos e o mantém linear para positivos.
![[Pasted image 20251217162453.png]]

### O Ponto de Inflexão (The Bend Point)

Quando aplicamos ReLU à saída de um neurônio ($z = wx + b$), o ponto onde a função deixa de ser zero e começa a crescer ocorre quando o argumento é zero:

$$wx + b = 0 \implies x = -\frac{b}{w}$$

Este valor de $x$ é o limiar de ativação. Abaixo dele, o neurônio está "morto"; acima, ele contribui linearmente.
![[Pasted image 20251217162937.png]]

É bom notar que um neurônio tem um bend, mas vários neurônios têm vários bends,  formando uma curva não lineear

### Por que a função tem o nome "Ativação"?
No seu cérebro real, um neurônio não fica enviando sinais o tempo todo. Ele acumula eletricidade vinda de outros neurônios. Se essa eletricidade passar de um certo limite (limiar), o neurônio dispara um pulso elétrico (chamado potencial de ação). Se não passar do limite, ele fica quieto. 
![[Pasted image 20251217174702.png]]
---

## 3. Arquitetura de Aproximação Universal

Como modelamos uma curva complexa usando funções que são essencialmente retas com dobras (piecewise linear)?

O Princípio da Superposição:

Ao utilizar múltiplos neurônios em uma Camada Oculta (Hidden Layer), cada um com seus próprios pesos ($w$) e viés ($b$), criamos múltiplos pontos de inflexão em locais diferentes do eixo $x$.

![[Pasted image 20251217122320.png]]

-  **Neurônio 1:** Ativa em 3 milhas (tráfego urbano).
    
- **Neurônio 2:** Ativa em 8 milhas (entrada da rodovia).
    
- **Neurônio 3:** Ativa em 15 milhas (velocidade de cruzeiro).

A camada de saída realiza uma combinação linear dessas ativações:

$$\hat{y} = v_1 \cdot \text{ReLU}(z_1) + v_2 \cdot \text{ReLU}(z_2) + v_3 \cdot \text{ReLU}(z_3) + b_{out}$$

A soma dessas funções "dobradas" resulta em uma função linear por partes que pode aproximar qualquer curva contínua suave (Teorema da Aproximação Universal). Quanto mais neurônios na camada oculta, mais suave é a aproximação.


### Algumas  outras funções de ativação
![[Pasted image 20251217180015.png]]

## 4. Implementação em PyTorch (`nn.Sequential`)

A implementação em código reflete a estrutura matemática de camadas alternadas (Linear -> Não-Linear -> Linear).

```python 
model = nn.Sequential(
    # Camada Oculta (Hidden Layer)
    # Entrada: 1 feature (distância)
    # Saída: 3 features (3 neurônios/caminhos distintos)
    nn.Linear(1, 3),

    # Função de Ativação (Element-wise)
    # Aplica max(0, x) em cada um dos 3 outputs anteriores
    nn.ReLU(),

    # Camada de Saída (Output Layer)
    # Entrada: 3 features (os sinais ativados da camada anterior)
    # Saída: 1 feature (previsão final de tempo)
    nn.Linear(3, 1)
)
```

**Análise Dimensional:**

1. Tensor de Entrada: $[N, 1]$
    
2. Após `Linear(1, 3)`: $[N, 3]$
    
3. Após `ReLU`: $[N, 3]$ (zeros onde o valor era negativo)
    
4. Após `Linear(3, 1)`: $[N, 1]$ (agregação final)
    

---

## 5. Outras Funções de Ativação

Embora a ReLU seja a dominante, outras funções são vitais para contextos específicos:

- **Sigmoid ($\sigma(x) = \frac{1}{1+e^{-x}}$):**
    
    - Mapeia valores para o intervalo $(0, 1)$.
        
    - Fundamental para saídas de probabilidade (classificação binária).
        
- **Tanh ($\tanh(x)$):**
    
    - Mapeia valores para $(-1, 1)$.
        
    - Útil quando os dados são centralizados em zero.