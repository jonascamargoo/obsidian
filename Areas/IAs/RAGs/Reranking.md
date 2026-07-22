O Reranking (Reclassificação) é uma etapa de **pós-recuperação** no pipeline RAG. Ele não é uma técnica de _busca_, mas sim um processo de _otimização_ que refina os resultados de uma busca inicial (como a de um Bi-Encoder) antes de enviá-los à LLM.

Seu objetivo é resolver o principal "trade-off" da busca semântica:

1. **Bi-Encoders (Busca Rápida):** São rápidos ($O(\log N)$ com HNSW), mas podem retornar resultados "semanticamente confusos" (ex: recuperar "A capital da França é Paris" para uma consulta sobre a "capital do Canadá").
    ![[Pasted image 20251102182732.png]]
2. **Cross-Encoders (Busca de Qualidade):** Têm uma qualidade de relevância "padrão-ouro" (pois analisam `Prompt+Documento`), mas são inviáveis para busca ($O(N)$).
    

O Reranking combina a **velocidade** do Bi-Encoder (para a busca inicial) com a **qualidade** do Cross-Encoder (para o refinamento).1

---

###  O Pipeline de Reclassificação

O processo de RAG com Reranking é executado em três etapas:

1. Etapa 1: Recuperação (Over-fetching)
    
    O retriever executa uma busca híbrida ou de Bi-Encoder, mas é configurado para "exagerar" (over-fetch) e trazer um conjunto inicial grande, porém ruidoso, de documentos.
    
    - Ex: `K_inicial = 50` (em vez de K=5).
        
2. Etapa 2: Reclassificação (Refinamento Caro)
    
    Esses 50 documentos recuperados (e apenas eles) são então passados para um modelo muito mais lento e caro (um Cross-Encoder) para uma re-pontuação. O Cross-Encoder executa 50 inferências (modelo(Prompt + Doc_1), modelo(Prompt + Doc_2), ... modelo(Prompt + Doc_50)) e gera um novo score de relevância muito mais preciso para cada um.
    
3. Etapa 3: Seleção Final
    
    O sistema reordena os 50 documentos com base nos novos scores do Cross-Encoder e, finalmente, seleciona o novo "Top K" (ex: K_final = 5).
    ![[Pasted image 20251102182639.png]]
	![[Pasted image 20251102182814.png]]
---

###  Arquiteturas de Reclassificação

Qualquer modelo que possa gerar um score de relevância para um par `(Prompt, Documento)` pode ser usado.

#### 1. Cross-Encoders (O Padrão)

Esta é a implementação mais comum e o uso ideal para a arquitetura Cross-Encoder. O problema de escalabilidade $O(N)$ (inviável para 1 milhão de documentos) torna-se um problema $O(K)$ (trivial para $K=50$ documentos). Você paga uma pequena penalidade de latência (para as 50 inferências) em troca de um enorme aumento na relevância.

#### 2. LLM-based Reranking (A Alternativa)

Uma técnica mais recente, conceitualmente idêntica ao Cross-Encoder.

- **Como Funciona:** Em vez de um Cross-Encoder especializado, você alimenta uma LLM padrão com o par `(Prompt, Documento)` e pede a ela para retornar um score de relevância numérico.
    
- **Trade-off:** É igualmente (ou mais) ineficiente que um Cross-Encoder e, portanto, também só pode ser usado como um reclassificador em um pequeno subconjunto de resultados.
    ![[Pasted image 20251102183039.png]]

---

### 🏁 Conclusão e Estratégia Prática

O Reranking é uma das melhorias mais fáceis e de maior impacto que podem ser adicionadas a um pipeline RAG.

- **Custo-Benefício:** O trade-off (aumento da latência vs. aumento da relevância) é **quase sempre vantajoso**.
    
- **Facilidade:** Em muitos Vector Databases modernos, adicionar um reclassificador pode ser tão simples quanto adicionar um único parâmetro à consulta de busca.
    
- **Heurística de Partida:** Uma boa regra de bolso é "buscar" (over-fetch) 15-25 documentos e reclassificá-los para selecionar o Top 5-10 final.