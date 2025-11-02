
A busca semântica "vanilla" (padrão) usa uma arquitetura **Bi-Encoder**, onde um único vetor representa o documento inteiro e outro vetor representa a consulta. Embora eficaz, arquiteturas mais sofisticadas existem para extrair resultados de maior qualidade, introduzindo _trade-offs_ de velocidade e custo.

### 1. O Padrão: Bi-Encoder (Foco na Velocidade)

Esta é a arquitetura padrão usada na maioria dos sistemas RAG.

- **Como Funciona:** O nome "Bi-Encoder" (Codificador Duplo) refere-se ao fato de que o documento e a consulta são processados (codificados) **separadamente**.
    
    1. **Ingestão (Offline):** Todos os $N$ documentos da base são vetorizados e indexados em um Vector DB (ex: HNSW).
        
    2. **Busca (Online):** O prompt é vetorizado, e o índice ANN é usado para encontrar os vetores de documentos mais próximos.
        
- **Prós:**
    
    - **Velocidade Extrema:** A busca é muito rápida (ex: $O(\log N)$ com HNSW), pois 99% do trabalho computacional (vetorização de documentos) é pré-processado.
        
- **Contras:**
    
    - **Qualidade Limitada:** O modelo nunca vê o prompt e o documento _juntos_. Ele perde interações contextuais profundas (ex: negações sutis, comparações).
        

---

### 2. O "Padrão Ouro": Cross-Encoder (Foco na Qualidade)

O Cross-Encoder é projetado para máxima relevância, sacrificando totalmente a velocidade.

- **Como Funciona:** Ele **concatena** o prompt e o documento e os passa _juntos_ por um modelo especializado.
    
    1. **Entrada:** `[PROMPT] + [DOCUMENTO]`
        ![[Pasted image 20251102175656.png]]
    2. **Saída:** Um **único score de relevância** (ex: 0 a 1), _não_ um vetor. Ele responde "o quão relevante este documento é para este prompt?"
        
        ![[Pasted image 20251102175750.png]]
- **Prós:**
    
    - **Qualidade de Relevância Superior:** Quase sempre supera um Bi-Encoder em métricas de busca, pois o modelo realiza uma análise contextual profunda da interação entre as palavras do prompt e do documento.
        
- **Contras:**
    
    - **Escalabilidade Terrível ( $O(N)$ ):** Não pode ser pré-processado. Para _cada consulta_, ele deve executar uma inferência completa do modelo para _cada documento_ na base. Se você tem 1 milhão de documentos, você precisa rodar 1 milhão de inferências por busca, tornando-o inviável para recuperação primária.
        

---

### 3. O Híbrido: ColBERT (Qualidade vs. Armazenamento)

ColBERT (Contextualized Late Interaction over BERT) tenta obter o melhor dos dois mundos: a qualidade de interação do Cross-Encoder com a eficiência de pré-processamento do Bi-Encoder.1

- **Como Funciona (Ingestão):** Em vez de um vetor por documento, ele cria **um vetor por _token_** do documento. Um documento de 2.000 tokens agora é representado por 2.000 vetores.
    
- **Como Funciona (Busca):**
    
    1. O prompt também é vetorizado (um vetor por token).
        
    2. Ocorre a **"Interação Tardia" (Late Interaction):** Para cada token do _prompt_, o sistema calcula a similaridade dele com _todos_ os tokens do _documento_ e encontra o score máximo (**MaxSim**).
        ![[Pasted image 20251102180621.png]]
    3. O score final do documento é a **soma** desses scores MaxSim (um para cada token do prompt).
        
        ![[Pasted image 20251102180808.png]]
- **Prós:**
    
    - **Alta Qualidade:** Atinge uma qualidade de relevância próxima à do Cross-Encoder, pois captura interações em nível de token.
        
    - **Razoavelmente Rápido:** Embora mais lento que um Bi-Encoder (pois precisa somar os scores MaxSim), ele ainda usa índices ANN para acelerar a busca e é viável para busca em tempo real.
        
- **Contras:**
    
    - **Custo de Armazenamento Massivo:** Este é o seu principal trade-off. Um Bi-Encoder armazena 1 vetor por documento; o ColBERT armazena milhares. Isso aumenta os custos de armazenamento e memória em ordens de magnitude.
        

---

### 📊 Resumo da Comparação

|**Arquitetura**|**Mecanismo de Score**|**Velocidade de Busca**|**Custo de Armazenamento**|**Qualidade (Relevância)**|
|---|---|---|---|---|
|**Bi-Encoder**|`dist( embed(P), embed(D) )`|Mais Rápida ( $O(\log N)$ )|Baixo (1 vetor/doc)|Boa|
|**Cross-Encoder**|`model( P + D )`|Mais Lenta ( $O(N)$ )|N/A (Não armazena vetores)|Excepcional (Gold Standard)|
|**ColBERT**|`sum( MaxSim( P_tokens, D_tokens ) )`|Rápida|Massivo (1 vetor/token)|Muito Alta|

**Conclusão:**

- **Bi-Encoder** é o padrão de-facto pela sua eficiência.
    
- **Cross-Encoder** é muito lento para busca (retrieval), mas sua qualidade o torna a ferramenta perfeita para uma etapa de **reclassificação (reranking)** (como veremos a seguir).
    
- **ColBERT** é uma opção de alta performance para casos de uso (ex: jurídico, médico) onde a precisão contextual é crítica e o custo de armazenamento massivo é justificável.