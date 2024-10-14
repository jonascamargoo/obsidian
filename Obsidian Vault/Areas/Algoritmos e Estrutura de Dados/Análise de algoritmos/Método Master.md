
* O método Máster provê uma “receita” para resolver recorrências do tipo T(n) = a T(n/b) + f(n) com a ≥1, b>1 constantes e f(n) função assintoticamente positiva.

* A ideia da recorrência é a divisão de um problema de tamanho n em a subproblemas, cada um de tamanho n/b;

* Os a subproblemas são resolvidos de forma recursiva, cada um com tempo T(n/b);

* O custo de dividir o problema e combinar os resultados dos subproblemas é descrito pela função f(n);

* O método master nos dá a complexidade, nao a função completa em si. Só uma das 3 condições será satisfeita, portanto, as outras duas necessariamente deveram ser falsas.


OBS: Ele não proporciona a função inteira, mas proporciona a complexidade. Exemplo, nao diz se é x² + 2x, mas diz que é x² e isso já é suficiente para uma análise mais prática.

##### teorema master

Seja T(n) = a T(n/b) + f(n) a≥1, b>1, f(n) ≥ 0 Então T(n) pode ser limitada assintoticamente como segue:

i. Se f(n) = O(n^((log a na base b) - ε ))  para alguma constante ε > 0, então T(n) = θ(n logba );

ii. Se f(n) = θ(n^(log a na base b), então T(n) = θ(n logba . log n);

iii.Se f(n) = Ω(n^((log a na base b) + ε )) para alguma constante ε > 0 e a.f(n/b) ≤ c.f(n) para alguma constante c < 1, então T(n) = θ(f(n)).