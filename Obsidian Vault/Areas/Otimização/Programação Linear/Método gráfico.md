## 🧠 Objetivo

Resolver **problemas de programação linear com duas variáveis** usando uma representação **gráfica** para encontrar a solução ótima (máxima ou mínima) de uma função objetivo. As restrições determinam uma região poligonal no plano , chamada região viável ou região de viabilidade . Essa região é construída usando as linhas de restrição , que são as linhas obtidas das desigualdades das restrições.

---

## Interpretação Geométrica

- Cada **restrição** define uma **região no plano**;
- A **região viável (ou factível)** é a interseção das regiões de todas as restrições;
- A **solução ótima** está **em um dos vértices** dessa região.

💡 _Dica visual_: Imagine uma área delimitada por retas — a resposta ideal sempre estará no "canto" dessa área!

---

## 🔎 Procedimento do Método Gráfico

### Passos para resolver graficamente:

1. **Desenhar cada restrição** como uma reta no gráfico;
2. **Determinar a região viável** (área comum a todas as restrições);
3. **Desenhar curvas de nível** da função objetivo (linhas com o mesmo valor de \( Z \));
4. **Movimentar essa curva na direção do gradiente** até tocar o último ponto dentro da região viável.

👉 O ponto onde a curva toca a região viável pela última vez é a **solução ótima*


```
Max Z = 2x + 3y funcao obj
sujeito a
  -x + y ≤ 5
   x + 4y ≤ 45
   2x + y ≤ 27
   3x – 4y ≤ 24
   x, y ≥ 0
```

Z(x, y) = 2x + 3y é a função objetivo, e as desigualdades são as restrições. Uma solução viável é um valor para variáveis que satisfaz todas as restrições, por exemplo, (x, y) = (2, 0). Chamamos as soluções viáveis de conjunto viável ou região viável ou factível. A figura a seguir apresenta graficamente elementos fundamentais do pl acima.

![[Pasted image 20250419181410.png]]

Procedimento da Solução Gráfica Seja um pl de maximização 

i. Desenhe a reta de cada restrição no gráfico. Identifique a região correspondente a cada restrição. 

ii. Identifique a região de soluções viáveis, isto é, a área do gráfico que simultaneamente satisfaz a todas as restrições. 

iii. Encontre a solução ótima pelo seguinte método: 
	a) Desenhe uma ou mais curvas de nível da função objetivo; 
	b) Desenhe o gradiente de Z; 
	c) Desenhe curvas de nível paralelas na direção indicada pelo gradiente de Z até que a curva toque a região de soluções viáveis em um único ponto (ou em um segmento). Este último ponto, que é o mais extremo, é a solução ótima. 

Em suma, o método gráfico na programação linear é usado para resolver problemas, encontrando o ponto “mais alto” ou “mais baixo” de interseção entre a linha de função objetivo e a região factível em um gráfico