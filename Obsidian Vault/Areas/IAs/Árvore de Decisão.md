

O algoritmo de Árvore de Decisão se destaca por sua simplicidade, interpretabilidade e poder preditivo. Utilizado tanto para tarefas de classificação quanto de regressão, este método simula o processo de tomada de decisão humano em uma estrutura intuitiva de árvore, tornando-o uma ferramenta valiosa para cientistas de dados e entusiastas da área.

### O que é uma Árvore de Decisão?

Em sua essência, uma Árvore de Decisão é um modelo de aprendizado supervisionado que utiliza uma estrutura de fluxograma em forma de árvore para tomar decisões. Ela é composta por:

- **Nós de Decisão (ou Nós Internos):** Representam um teste em um atributo (uma "pergunta").
    
- **Ramos:** Indicam o resultado do teste em um nó de decisão.
    
- **Nós Folha (ou Nós Terminais):** Representam um resultado final (uma classificação ou um valor).
    

O processo se inicia no **nó raiz**, que engloba todo o conjunto de dados. A partir dele, o algoritmo seleciona o melhor atributo para dividir os dados em subconjuntos mais homogêneos, criando novos nós de decisão e ramos. Esse processo de divisão continua recursivamente até que um critério de parada seja atingido, como a profundidade máxima da árvore ou a impossibilidade de novas divisões que melhorem o modelo.

### A Busca pela Pureza: O Coração da Árvore de Decisão

O objetivo principal de uma Árvore de Decisão é criar nós folha que sejam os mais "puros" possíveis. Em um contexto de classificação, um nó é considerado puro se todas as amostras de dados pertencentes a ele são da mesma classe. Para medir a impureza de um nó e, consequentemente, decidir qual atributo resultará na melhor divisão, são utilizadas métricas como:

- **Índice de Gini:** Mede a probabilidade de um elemento ser classificado incorretamente se fosse rotulado aleatoriamente de acordo com a distribuição das classes no nó. Um valor de Gini igual a 0 indica pureza total.
    
- **Entropia e Ganho de Informação:** A entropia mede o grau de desordem ou incerteza em um nó. O Ganho de Informação calcula a redução na entropia após a divisão de um nó por um determinado atributo. O algoritmo busca a divisão que maximize o ganho de informação.
    

A cada divisão, o algoritmo escolhe o atributo que resulta nos subconjuntos com a menor impureza (ou maior pureza), construindo assim uma árvore que segmenta os dados de forma cada vez mais específica.

### O Dilema da Profundidade: Quando a Perfeição se Torna um Problema

A busca incessante pela pureza absoluta em todos os nós folha leva a um crescimento significativo na altura (ou profundidade) da árvore (árvore de decisão é um algoritmo exaustivo). Cada nova divisão, por mais que aumente a pureza em relação aos dados de treinamento, adiciona um novo nível de complexidade ao modelo. É neste ponto que surge um dos principais desafios das Árvores de Decisão: o **overfitting**, ou sobreajuste.

Quando uma árvore se torna excessivamente profunda, ela começa a "memorizar" os dados de treinamento, incluindo seus ruídos e particularidades. As regras criadas nos nós mais profundos se aplicam a um número cada vez menor de amostras, perdendo a capacidade de generalização para novos dados, nunca antes vistos pelo modelo. Em outras palavras, o modelo se torna um **sistema especialista** no conjunto de dados de treinamento, mas falha em prever resultados para dados do mundo real.

![[Pasted image 20250808225025.png]]Exemplo de nó (esquerda) menos puro

![[Pasted image 20250808225152.png]]
Exemplo com nós mais puros (nó esquerdo, na branch de Cor). Tem menos variedades de formatos, porém a chance de acertar é maior. Temos mais informações sobre o que é uma Weissibier do que uma Pilsen, já que temos dois possíveis formato delas.

Imagine uma árvore de decisão para aprovação de crédito. Uma árvore muito profunda poderia criar uma regra como: "SE o cliente tem entre 30 e 32 anos, é do sexo masculino, possui dois cartões de crédito E o nome de seu animal de estimação é 'Rex', ENTÃO o crédito é aprovado". Embora essa regra possa ser perfeitamente acurada para uma única instância nos dados de treinamento, ela é completamente inútil e não generalizável para a população em geral.

Essa perda de amostras em nós cada vez mais específicos torna o sistema frágil e pouco robusto. A alta variância do modelo faz com que pequenas alterações nos dados de treinamento possam resultar em uma árvore completamente diferente.

Para combater o overfitting, técnicas como a **poda (pruning)** são empregadas. A poda consiste em remover partes da árvore (ramos e nós) que fornecem pouco poder preditivo, resultando em um modelo mais simples e com melhor capacidade de generalização. Outra abordagem é limitar a profundidade máxima da árvore ou definir um número mínimo de amostras por nó folha.

## Exemplo de código

```python

# %%

# Carregamento dos dados

import pandas as pd


df = pd.read_excel("data/dados_frutas.xlsx")

df # pq o df solto aqui? -> Quando a última linha de uma célula é uma variável ou um objeto (sem estar dentro de um print()), o ambiente automaticamente "inspeciona" esse objeto e exibe sua representação visual mais rica como a saída da célula.

# %%

# Preparação dos Dados para o Modelo
  

from sklearn import tree #scikit-learn é a maior lib de ML em python - im importing its decicion tree and its classifier

  

arvore = tree.DecisionTreeClassifier(random_state=42) # Cria uma "instância" vazia de um modelo de Árvore de Decisão para classificação. random_state=42 é um parâmetro para garantir que, se o algoritmo precisar de alguma aleatoriedade, os resultados sejam sempre os mesmos toda vez que o código for rodado, garantindo a reprodutibilidade.

  

y = df['Fruta'] # Separação da nossa variável-alvo. y é o que queremos que o modelo aprenda a prever. Neste caso, é a coluna "Fruta" da nossa tabela

  

caracteristicas = ["Arredondada","Suculenta",'Vermelha','Doce'] # Separação da nossa variável-alvo. y é o que queremos que o modelo aprenda a prever. Neste caso, é a coluna "Fruta" da nossa tabela.

  

X = df[caracteristicas] # Separação das nossas variáveis preditoras (features). X representa os dados que o modelo usará para fazer a previsão. Aqui, estamos selecionando apenas as colunas com as características da fruta.

  

# Aqui X e Y devem ter o mesmo número de linhas, pois cada linha de X corresponde a uma linha de y. Ou seja, cada fruta tem suas características e seu nome associado.

X

  

# %%

# ISSO AQUI E MACHINE LEARNING!!!!

arvore.fit(X, y) # O método .fit() treina o modelo. Ele analisa os dados X (características) e y (nomes das frutas) e "aprende" as regras e padrões que conectam as características a cada tipo de fruta. Por exemplo, ele pode aprender que "se 'Vermelha' for 1 e 'Arredondada' for 1, a chance de ser uma Maçã é alta".

  

# %%

# Fazendo uma Previsão Simples

arvore.predict([[1,1,1,0]]) # Agora usamos o modelo treinado para fazer uma previsão. Estamos fornecendo um novo dado para o modelo: uma fruta que não é Arredondada (0), não é Suculenta (0), não é Vermelha (0) e não é Doce (0). O modelo usará as regras que aprendeu para classificar essa nova fruta.

  

# %%

  

import matplotlib.pyplot as plt

  

plt.figure(dpi=400, figsize=[4,4])

  

tree.plot_tree(arvore,

feature_names=caracteristicas,

class_names=arvore.classes_,

filled=True)


#%%

proba = arvore.predict_proba([[1,1,1,1]])[0]
pd.Series(proba, index=arvore.classes_)

```


![[Pasted image 20250810133628.png]]Representação da árvore de decisão gerada