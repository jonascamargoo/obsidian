
### Teorema de Bayes

O classificador Naive Bayes é um algoritmo que se baseia nas descobertas de Thomas Bayes para realizar predições em aprendizagem de máquina. O termo “naive” (ingênuo) diz respeito à forma como o algoritmo analisa as características de uma base de dados: ele assume que as features são independentes entre si. Seu desempenho também é consideravelmente bom com classes múltiplas e ele funciona melhor com features categóricos (palavras) do que com numéricos.

o problema de classificação se encaixa na categoria de problema supervisionado, pois gera uma predição e um modelo como resultado, sendo necessária a supervisão de profissionais. Ou seja, quem treina passa os dados e as saídas dos dados de treinamento, informando ao sistema exatamente o que ele deve aprender.

O algoritmo é baseado no **Teorema de Bayes**, que descreve a probabilidade de um evento A ocorrer, dado que o evento B ocorreu. Matematicamente, é expresso como (sem considerar a correlação entre os fatores):

A equação do Teorema de Bayes é dada por: 

$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}$


- P(A∣B) é a probabilidade posterior de A, dado B.
- P(B∣A) é a probabilidade de B, dado A (probabilidade de observação).
- P(A) é a probabilidade de A antes de observar B (probabilidade a priori de A).
- P(B) é a probabilidade de B.

## Aplicação

Uma aplicação prática do **Naive Bayes** pode ser em **filtragem de spam em e-mails**. O objetivo é classificar uma mensagem de e-mail como "spam" ou "não spam" (ham) com base nas palavras que aparecem nela.

**Dados de Treinamento**: Vamos supor que temos um conjunto de e-mails já classificados como "spam" ou "não spam" e cada e-mail é representado por um conjunto de palavras.

|E-mail|Classificação|Palavras|
|---|---|---|
|E-mail 1|Não Spam|"Olá", "amigo", "como", "vai"|
|E-mail 2|Spam|"promoção", "oferta", "clique", "aqui"|
|E-mail 3|Não Spam|"reunião", "agenda", "empresa"|
|E-mail 4|Spam|"compre", "agora", "desconto"|
|E-mail 5|Não Spam|"feliz", "aniversário", "foto"|

**Objetivo**: Dado um novo e-mail (por exemplo, "oferta especial para você, clique agora"), queremos determinar se ele é spam ou não spam.

#### Passo 1: Calcular as probabilidades a priori das classes

Primeiro, calculamos a probabilidade de cada classe (spam e não spam) com base no conjunto de treinamento.

$P(\text{Spam}) = \frac{\text{Número de e-mails spam}}{\text{Total de e-mails}} = \frac{2}{5} = 0.4$


$P(\text{Spam}) = \frac{\text{Número de e-mails spam}}{\text{Total de e-mails}} = \frac{3}{5} = 0.6$


#### Passo 2: Calcular as probabilidades condicionais das palavras

Agora, calculamos as probabilidades de cada palavra aparecer em um e-mail dado a classe (spam ou não spam).

Por exemplo, para a palavra **"oferta"**, a probabilidade condicional de ela aparecer dado que o e-mail é **spam** seria:

$P(\text{"oferta"}|\text{Spam}) = \frac{\text{Número de e-mails spam contendo "oferta"}}{\text{Número total de e-mails spam}} = \frac{1}{2} = 0.5$

E para **"oferta"** dado que o e-mail é **não spam**:

$P(\text{"oferta"}|\text{Spam}) = \frac{\text{Número de e-mails spam contendo "oferta"}}{\text{Número total de e-mails spam}} = \frac{0}{3} = 0$

Repetimos esse cálculo para todas as palavras no e-mail de entrada.

#### Passo 3: Aplicar o Teorema de Bayes

Para classificar o novo e-mail como "spam" ou "não spam", usamos o Teorema de Bayes:

$P(\text{Spam}|X) = \frac{P(X|spam) \cdot P(\text{Spam})}{P(X)}$

$P(\text{Não Spam}|X) = \frac{P(X|Não spam) \cdot P(\text{Não Spam})}{P(X)}$


#### Passo 4: Comparar as probabilidades

Com as probabilidades calculadas para cada classe, escolhemos a classe com a maior probabilidade como a classificação final.

Se $P(Spam∣X)>P(Não Spam∣X)$, o e-mail é classificado como spam. Caso contrário, é classificado como não spam. 



