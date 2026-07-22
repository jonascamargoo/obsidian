---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2024-10-14'
---

## Keyword Search TF-IDF

A **Keyword Search** (Busca por Palavra-Chave) é uma técnica fundamental de recuperação de informação que classifica documentos com base no compartilhamento de palavras com a consulta (prompt). A premissa é que a relevância é proporcional à sobreposição de termos.
![[Pasted image 20251103133509.png]]

---

### 1. O Fundamento: Bag of Words (BoW) e o Inverted Index

O Keyword Search ignora a ordem gramatical e trata todo texto (documento ou consulta) como um **"Bag of Words" (Saco de Palavras)**. O que importa é _quais_ palavras existem e _quantas vezes_ elas aparecem.

- **Vetores Esparsos (Sparse Vectors):** Cada texto é convertido em um vetor onde o comprimento é o tamanho total do vocabulário do sistema (ex: 50.000 palavras). Cada posição no vetor corresponde a uma palavra, e o valor é a contagem (frequência) daquela palavra no texto. A maioria desses vetores é preenchida com zeros.
	![[Pasted image 20251103134145.png]]
    
- **Term-Document Matrix (Inverted Index):** Para a base de conhecimento, esses vetores esparsos são pré-computados e organizados em uma matriz onde as **linhas são os termos (palavras)** e as **colunas são os documentos**.
    
    - Isso é chamado de **Inverted Index (Índice Invertido)** porque permite uma consulta $O(1)$ (ou muito rápida) de `palavra -> documentos que a contêm`, em vez da consulta normal de `documento -> palavras que ele contém`.
        ![[Pasted image 20251103134101.png]]

---

### 2. A Evolução do Algoritmo de Scoring (Pontuação)

Quando uma consulta é recebida, ela também é transformada em um vetor esparso. O objetivo é pontuar cada documento (coluna) com base na consulta. O algoritmo de pontuação evoluiu para resolver problemas sucessivos:

#### Abordagem 1: Scoring Binário

- **Como Funciona:** Para cada palavra-chave na consulta, encontre sua linha no índice. Dê 1 ponto para cada documento que contém essa palavra (contagem > 0). O score final é a soma dos pontos.
    ![[Pasted image 20251103134444.png]]
- **Problema:** Não captura a frequência. Um documento que menciona "pizza" 10 vezes (provavelmente sobre pizza) tem a mesma pontuação que um que a menciona 1 vez (passando).
    

#### Abordagem 2: Term Frequency (TF)

- **Como Funciona:** Em vez de dar 1 ponto, dê ao documento a pontuação que está na célula — ou seja, a **contagem** da palavra-chave. O score final é a soma das contagens de todas as palavras-chave.
    ![[Pasted image 20251103134843.png]]
- **Problema:** Favorece documentos longos. Um livro de 500 páginas (documento longo) quase sempre terá mais menções de palavras-chave do que um artigo de 1 página (documento curto), mesmo que o artigo seja _mais relevante_ sobre o tema.
    

#### Abordagem 3: TF Normalizado

- **Como Funciona:** Calcula o score de TF (Abordagem 2) e o divide pelo número total de palavras no documento.
    
- **Resultado:** O score agora representa a _proporção_ do texto que é dedicada às palavras-chave, nivelando o campo entre documentos longos e curtos.	$$ score = \left(\frac{\text{number of keyowrd occurrences}}{\text{total words in documents}}\right)$$
- **Problema:** Trata todas as palavras com o mesmo peso. Palavras de preenchimento ("filler words") como "o", "a", "sem" recebem a mesma pontuação que termos raros e significativos como "pizza" ou "forno".

---

### 3. A Solução Padrão: TF-IDF

O TF-IDF resolve o problema final ao introduzir um peso que mede a _raridade_ de uma palavra: **Inverse Document Frequency (IDF)**.

- **Cálculo do IDF:** O IDF é um valor pré-calculado para _cada palavra_ no vocabulário. A fórmula conceitual é:
    
    $$ IDF(\text{palavra}) = \log\left(\frac{\text{Total de Documentos na Base}}{\text{Nº de Documentos que Contêm a palavra}}\right)$$
    
- **O Efeito:**
    
    - Palavras comuns (ex: "o", "a") aparecem em quase todos os documentos. O denominador é grande, a fração é próxima de 1, e o `log(1)` é 0. Elas recebem peso **zero** ou muito baixo.
        
    - Palavras raras (ex: "pizza") aparecem em poucos documentos. O denominador é pequeno, a fração é grande, e o `log` dá a elas um peso **alto**.
        
- **Matriz TF-IDF:** O Inverted Index é atualizado. O valor em cada célula não é mais apenas a contagem (TF), mas sim `TF * IDF`.
    
- **Scoring Final (TF-IDF):** O score de um documento para uma consulta é a **soma dos valores TF-IDF** em sua coluna para cada palavra-chave da consulta.

    $$\text{Score}_{\text{Final}}(\text{doc, query}) = \sum_{\text{word} \in \text{query}} \left( \text{TF}(\text{word, doc}) \times \text{IDF}(\text{word}) \right)$$
    ![[Pasted image 20251103141342.png]]

**Resultado:** Os documentos que recebem a pontuação mais alta são aqueles que usam as palavras-chave da consulta _frequentemente_ (alto TF) e, crucialmente, onde essas palavras-chave são _raras e distintivas_ (alto IDF).

---

### 4. Limitações e Próximo Passo

Embora o TF-IDF seja a base do keyword search, sistemas modernos usam uma versão ligeiramente refinada e com melhor desempenho chamada **BM25**, que otimiza como a frequência dos termos (TF) e o comprimento do documento são normalizados.