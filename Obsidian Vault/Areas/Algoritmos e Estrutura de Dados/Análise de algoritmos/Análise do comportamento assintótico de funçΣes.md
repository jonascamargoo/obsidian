
### Principais Técnicas de Análise de Algoritmo

Existem várias técnicas para medir o custo de utilização de um algoritmo. Aqui estão as principais técnicas:

1.  Análise de tempo: essa técnica mede o tempo necessário para executar um algoritmo em diferentes tamanhos de entrada. É importante ter em mente que o tempo de execução pode variar de acordo com o hardware e o ambiente de execução. Uma vantagem dessa técnica é que ela fornece uma medida quantitativa direta do desempenho do algoritmo. A desvantagem é que o tempo de execução pode ser afetado por fatores externos e não captura a complexidade do algoritmo de forma precisa.
    
2.  Análise de espaço: essa técnica mede a quantidade de memória necessária para executar um algoritmo em diferentes tamanhos de entrada. A vantagem dessa técnica é que ela fornece uma medida quantitativa direta da eficiência de uso de memória do algoritmo. A desvantagem é que o espaço de memória pode ser limitado por fatores externos, como a capacidade do hardware, e pode variar de acordo com o ambiente de execução.
    
3.  Análise assintótica: essa técnica mede a complexidade do algoritmo em termos de sua ordem de crescimento à medida que o tamanho da entrada aumenta. A vantagem dessa técnica é que ela fornece uma medida abstrata e independente do ambiente de execução do algoritmo. A desvantagem é que ela não fornece uma medida direta do tempo ou espaço necessário para executar o algoritmo em tamanhos de entrada específicos.
    
4.  Análise de pior caso: essa técnica mede o tempo ou espaço necessário para o pior caso de entrada possível. A vantagem dessa técnica é que ela fornece uma garantia de desempenho para todos os casos de entrada possíveis. A desvantagem é que o pior caso pode ser muito raro ou até mesmo impossível em muitos casos.
    
5.  Análise amortizada: essa técnica mede o custo médio de uma sequência de operações em um algoritmo, em vez do custo de cada operação individualmente. A vantagem dessa técnica é que ela leva em conta o comportamento geral do algoritmo em uma sequência de operações, em vez de cada operação individualmente. A desvantagem é que ela pode ser menos precisa do que a análise de pior caso em algumas situações


#### Big O


Dizemos que f(x) = O(g(n)) caso g(n) domine assintoticamente f(x). Em outras palavras, ao analisar valores de n -> inf, percebe-se que haverá um valor n o qual g(x), vezes uma constante c, é maior ou igual a f(x). Assim: f(n) <= c * g(n), pra tal valor c constante e n maior que um n0.


![[bc10b2da-91c9-4e81-ba35-2c89e04aed40.jpeg]]

Podemos provar essa relação tabulando os valores de n, até achar um valor de n que satisfaça c vezes g(n) >= f(n). Exemplo: 3n² + n é O(n²)

##### Algumas propriedades da função O

(i) f(n) = O(f(n))
(ii) c.O(f(n)) = O(f(n)), c constante
(iii) O(f(n)) + O(f(n)) = O(f(n))
(iv) O(O(f(n)) = O(f(n))
(v) O(f(n)) + O(g(n)) = O(Max(f(n), g(n)))
(vi) O(f(n)). O(g(n)) = O(f(n).g(n))
(vii) O(f(n).g(n)) = f(n) . O(g(n))

#### Pequeno o

a notação f(n) = o(g(n)) significa uma relação assintótica estrita, ou seja, há uma constante c para um dado valor de n que f(n) < g(n) vezes c. Já nesse caso percebe-se que é apenas menor e, não, menor ou igual.

Ex: provando que (n+1)² é O(n²), ou seja, se f(n) = (n+1)² e g(n) = n², f(n) = O(g(n²))

n = 0 -> f(n) = 1, g(n) = 0
n = 1 -> f(n) = 4, g(n) = 1
n = 2 -> f(n) = 9, g(n) = 4
n = 3 -> f(n) = 16, g(n) = 9

percebe-se que f(n) <= c.g(n) se c = 2 e para todo n >= 3

##### agora por indução matemática

passo base:
	|(n+1)²| <= c * | n²|, para c = 2 e n>= 3
	|(n+1)| <= 2|n²|, p/ n>=3

hipótese:
	n = k
	(k+1)² <= 2k²,   p/ n >= 3

passo indutivo:
	n = k + 1
	((k+1)+1)² <= 2(k+1)²
	(k+2)² <= 2(k+1)²
	(k+2)² = k² +4k + 4 = (k² +2k + 1) + (2k+3) = (k+1)² + (2k+3) <- lado esquerdo
	
	agora, como a hipótese é (k+1)² <= 2k², substituimos nesse lado esquerdo:

	2k²+(2k+3) <= 2(k+1)²
	2k²+2k+3 <= 2k²+4k+2, portanto: (n+1)² é O(n²) - afirmação verdadeira
	

ex 2:  f(n) = 10n. Prova f(n) = O(n * logn)

n= 0 -> f(n) = 0, nlog(n) = 0
n = 1 -> f(n) = 10, nlog(n) = 0
n = 2 -> f(n) = 20, nlog(n) = 0,6
n = 3 -> f(n) = 30, nlog(n) = 1,43
n = 4 -> f(n) = 40, nlog(n) = 2,4
n = 5 -> f(n) = 50, nlog(n) = 3,49
n = 10 -> f(n) = 100, nlog(n) = 10
n = 100 -> f(n) = 100, nlog(n) = 200
n = 1000 -> f(n) = 10.000, nlog(n) = 3000

percebe-se que é válido para c = 10 e n >= 10

#### Ordem Ω (Omega)

A expressão " f = O (g) " tem o significado matemático de " f ≤
precisamos de um conceito que tenha o significado de " f ≥ g ".

Dadas funções assintoticamente não-negativas f e g , dizemos que f está na ordem Omega de g , e escrevemos f = Ω (g) , ou f ∈ Ω (g), se f(n) ≥ c · g(n) para algum c positivo e para todo n suficientemente grande. Em outras palavras, existe um número positivo c e um número positivo n 0 tais que f(n) ≥ c · g(n) para todo n ≥ n 0 . Neste caso, dizemos que g(n) é um limite assintótico inferior para f(n).

![[grafico-omega.jpeg]]

Ex:

f(n) = 2n, prove que f(n)=  Ω(n^m) para m > 1
2n >= c * |n^m|

uma função linear nao será maior que uma exponencial assintoticamente


Ex:

f(n) = (n)^(1/4), prove que f(n) = Ω(ln(n))

n = 10², f(n) = 3.16, ln(n) = 4.6
n = 10³, f(n) = 5.62, ln(n) = 6,9
n = 10⁴, f(n) = 10, ln(n) = 9.21
n = 10⁵, f(n) = 17.7, ln(n) = 11, 51
n = 10⁶, f(n) = 31.6, ln(n) = 13.8

percebe-se que elas vao se distanciando para c = 1 e n>= 10⁴

#### Ordem Θ (Theta)

Dizemos que f e g estão na mesma ordem Theta e escrevemos f = Θ (g) ou f ∈ Θ (g) se f(g) e f = Ω (g) . Trocando em miúdos, f= Θ (g) significa que existem números positivos c 1 e c 2 tais que c 1 ∙g(n) ≤ f(n) ≤ c 2 ∙g(n) para todo n suficientemente grande (n ≥ n 0 )

![[grafico-theta.jpeg]]

Ex:

f(n) = log (n^10), mostre que é θ(log n)?

c1 * log(n) <= 10 * log(n) <= c2 * log(n)

verdadeiro para c1 <= 10 && c2 >= 10


### Classes de comportamento assintótico

do melhor para o pior algoritmo:

O(1) < O(log log n) < O(log n) < O(n 1/10 ) < O(Ön) <
O(n) <... < O (n log n) < O(n 2 ) < O(n 5 ) < O(2 n ) <
O(n!)
