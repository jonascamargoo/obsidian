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


Para um neurônio com múltiplas entradas, a função é uma soma ponderada das entradas mais um bias:

$f(x_1,x_2,...,x_n)=w_1∗x_1+...+w_n∗x_n+b$

Esta soma ponderada, que representa o potencial de ativação do neurônio, para n igual a 3, é calculada como:

![[Pasted image 20250702090929.png]]
onde cada neurônio tem seu u

### Algoritmo de Treinamento do Perceptron

- **Inicialização:** Antes do início da primeira época, inicialize os pesos $w_i$​ com valores pequenos e randômicos (-0.1 e 0.1).
    
- **Épocas de Treinamento:** Enquanto não encontrar uma condição de parada, faça:
    - Para cada par de treinamento `<x,y>`, onde `x` é o vetor de entrada e `y` é a saída desejada, execute os seguintes passos:
        
        1. **Cálculo da Saída:** Execute o vetor `x` na rede neural para encontrar a saída $o_k$, k é a dimensão de saída;
            
        2. **Cálculo do Delta:** Para cada peso wi​k, calcule a sua variação (Δwi​k). A regra de atualização é: $Δw_ik​ = η(y_k−o_k)xi$​, tal que η é o coef de aprendizado e $y_k−o_k$ é a saída desejada menos a saída obtida. Teremos um delta por peso
         
        3. **Atualização dos Pesos:** Para cada peso w_i​k, calcule seu novo valor$$\overline{\overline{w_ik}} = \overline{\overline{w_ik}} + \overline{\overline{Δw_ik$}}$$
