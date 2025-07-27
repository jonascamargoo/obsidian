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

