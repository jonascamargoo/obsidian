---
tipo: conceito
area: IAs
tags:
- ia/rag
- ia/llmops
criada: '2026-02-23'
---

**Data:** 23/02/2026

**Tópico:** #MachineLearning #Optimization #VectorDatabase #LLM #ComputerEngineering

---

## 🧩 1. O Conceito: Precisão vs. Performance

A quantização é o processo de substituir pesos de modelos (LLMs) ou valores de vetores (_embeddings_) por tipos de dados de **menor precisão**.

- **Analogia:** Funciona como a compressão de imagem (ex: passar de 24-bit para 8-bit), onde artefatos visuais surgem, mas o ganho de memória é massivo.
    
- **Benefício:** Reduz o tamanho do modelo, o custo de inferência e a latência, muitas vezes com impacto mínimo na qualidade.
    

---

## 🧠 2. Quantização em LLMs

Parâmetros típicos de LLMs usam **16-bit (FP16)**. Para modelos com bilhões de parâmetros, a exigência de VRAM é proibitiva.

- **Compressão:** Reduz-se de 16-bit para **8-bit** ou **4-bit**.
    
- **Impacto:** Redução significativa da memória da GPU necessária e geração de texto mais rápida, com perdas de performance mínimas em benchmarks padrão.
    

---

## 📏 3. Quantização de Vetores (Embedding Vectors)

Um vetor de 768 dimensões em **32-bit (FP32)** ocupa ~3 KB. Em escalas de bilhões de vetores, isso exige RAM caríssima.

### Integer Quantization (INT8)

Transforma floats de 32-bit em inteiros de 8-bit, reduzindo o tamanho em **4x**, mas mantendo praticamente o mesmo resultado.

**Algoritmo de Conversão:**

1. Identifica-se o **Mínimo** e **Máximo** de cada dimensão nos dados.
    
2. Divide-se esse intervalo em **256 seções** (capacidade de 8 bits).
    
3. Atribui-se a cada float o índice da seção (0-255) em que ele se encontra.
    
4. Para reconstrução (aproximada), armazena-se o valor mínimo e a largura da seção.
    
![[Pasted image 20260223155122.png]]
### Binary Quantization (1-bit)

Nível extremo que reduz o tamanho em **32x**.

- Cada dimensão vira **0 ou 1**, indicando apenas se o valor original era positivo ou negativo.
    
- **Estratégia de Rescoring:** Realiza-se a busca rápida com vetores de 1-bit e depois faz-se o _ranking_ refinado dos top-K resultados usando os vetores originais de 32-bit.
    

---

## 🪆 4. Matryoshka Embeddings (Nesting Dolls)

Técnica onde as dimensões do vetor são ordenadas por **densidade de informação** (variância estatística).

- **Propriedade:** As primeiras dimensões (ex: as primeiras 100 de 1000) contêm a maior parte da informação relevante.
    
- **Flexibilidade:** Permite truncar o vetor conforme a necessidade do ambiente:
    
    - **Baixa fidelidade:** Usa apenas as primeiras dimensões para busca ultra-rápida.
        
    - **Alta fidelidade:** Busca inicial com 100 dimensões e refinamento (_rescoring_) buscando as outras 900 de uma memória mais lenta e barata.
        

---

## 📊 Tabela Comparativa de Tipos de Dados

|**Tipo de Dado**|**Tamanho por Dimensão**|**Ganho de Espaço**|**Uso Comum**|
|---|---|---|---|
|**FP32**|32 bits|1x (Base)|Treinamento e Precision Search|
|**FP16**|16 bits|2x|Pesos de LLM padrão|
|**INT8**|8 bits|4x|Quantização padrão de vetores|
|**4-bit**|4 bits|8x|Execução local de LLMs grandes|
|**Binary**|1 bit|32x|Busca vetorial em escala massiva|

---

> [!TIP] **Conclusão para Engenharia**
> 
> A recomendação prática é sempre experimentar com modelos quantizados em **8 ou 4 bits**. Os ganhos de custo e latência geralmente compensam a pequena queda de precisão (muitas vezes de apenas alguns pontos percentuais em métricas como Recall@K).