---
tipo: conceito
area: IAs
tags:
- ia/nlp
criada: '2025-02-25'
---

## O que é?

O pré-processamento de textos é uma etapa crucial na execução da análise de sentimentos, pois ajuda a limpar e normalizar os dados de textos, facilitando a análise. A etapa de pré-processamento envolve uma série de técnicas que ajudam a transformar dados de textos brutos em um formato que pode ser usado para análise. Algumas técnicas comuns de pré-processamento de textos incluem tokenização, remoção de palavras irrelevantes (stop words), stemming e lematização.

![[Pasted image 20250225093250.png]]


A **tokenização** é um processo fundamental no processamento de linguagem natural (PLN) e na análise de sentimentos. Ela consiste em dividir um texto em unidades menores chamadas **tokens**, que podem ser palavras, frases ou até caracteres, dependendo da abordagem utilizada.

### Importância da Tokenização:

- Permite estruturar textos brutos para análise computacional.
- Facilita a identificação de palavras-chave, padrões e sentimentos.
- Prepara os dados para outras etapas do PLN, como stemming, lematização e vetorização.

### Como funciona a Tokenização:

No **NLTK (Natural Language Toolkit)**, uma biblioteca popular de PLN em Python, a função `word_tokenize()` é frequentemente usada para dividir textos em palavras e sinais de pontuação. Exemplo:

``` python
from nltk.tokenize import word_tokenize

texto = "A tokenização é essencial na análise de sentimentos!"
tokens = word_tokenize(texto)
print(tokens)

output
['A', 'tokenização', 'é', 'essencial', 'na', 'análise', 'de', 'sentimentos', '!']

```

### Palavras irrelevantes

A remoção de palavras irrelevantes (stop words) é uma etapa crucial de pré-processamento de textos na análise de sentimentos que envolve a remoção de palavras comuns e sem importância que provavelmente não transmitem muito sentimento. Palavras irrelevantes são palavras muito comuns em um idioma e que não têm muito significado, como "e", "o" e "de". Essas palavras podem causar ruído e distorcer a análise se não forem removidas.

Ao remover as palavras irrelevantes, as palavras restantes no texto têm maior probabilidade de indicar o sentimento que está sendo expresso. Isso pode ajudar a melhorar a precisão da análise de sentimentos. O NLTK fornece uma lista integrada de palavras irrelevantes para vários idiomas, que pode ser usada para filtrar essas palavras dos dados de textos.

### Stemming e lematização

Stemming e lematização são técnicas usadas para reduzir as palavras à sua raiz. O stemming envolve a remoção dos sufixos das palavras, como "ing" ou "ed", para reduzi-las à sua forma básica. Por exemplo: a palavra "jumping" seria derivada de "jump".

A lematização, no entanto, envolve a redução de palavras à sua forma básica segundo sua classe gramatical. Por exemplo: a palavra "jumped" seria lematizada para "jump", mas a palavra "jumping" seria lematizada para "jumping", pois está no gerúndio.

## Modelo bag of words

O modelo bag of words (saco de palavras) é uma técnica usada no processamento de linguagem natural (PLN) para representar dados de textos como um conjunto de recursos numéricos. Nesse modelo, cada documento ou texto é representado como um "saco" de palavras, com cada palavra no texto representada por um atributo (feature) ou dimensão separada no vetor resultante. O valor de cada atributo é determinado pelo número de vezes que a palavra correspondente aparece no texto.

O modelo bag of words é útil em PLN porque nos permite analisar dados de textos usando algoritmos de machine learning, que normalmente exigem entrada numérica. Ao representar dados de textos como atributos numéricos, podemos treinar modelos de machine learning para classificar textos ou analisar sentimentos.

O exemplo da próxima seção usa o modelo NLTK Vader para análise de sentimentos no conjunto de dados de clientes da Amazon. Neste exemplo específico, não precisamos executar essa etapa porque a API NLTK Vader aceita textos como entrada em vez de vetores numéricos, mas, se você estivesse criando um modelo de machine learning supervisionado para prever sentimentos (supondo que você tenha dados rotulados), teria que transformar os textos processados em um modelo bag of words antes de treinar o modelo de machine learning.

![[Pasted image 20250225094230.png]]