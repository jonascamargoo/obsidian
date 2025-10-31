A busca híbrida (Hybrid Search) não é uma técnica única, mas sim um **pipeline orquestrado** que combina os pontos fortes de diferentes métodos de recuperação para mitigar suas fraquezas individuais. O objetivo é criar um sistema de recuperação mais robusto e ajustável.

O pipeline geralmente se baseia em três componentes principais.

### 1. Os Componentes da Busca Híbrida

#### 1. Keyword Search (ex: BM25)

- **Como Opera:** Pontua e classifica documentos com base na correspondência exata (ou por _stemming_) das palavras-chave da consulta.
    
- **Pontos Fortes:** Rápido, fácil de implementar e excelente para consultas que contêm termos técnicos, JIDs (Identificadores Únicos) ou nomes de produtos. Garante que, se a palavra exata existir, ela será encontrada.
    
- **Fraqueza:** Falha totalmente em sinônimos ou consultas conceituais (significados semelhantes, palavras diferentes).
    

#### 2. Semantic Search (Busca Vetorial)

- **Como Opera:** Transforma a consulta e os documentos em vetores de embedding, classificando com base na proximidade (ex: similaridade de cosseno) em um espaço vetorial.
    
- **Pontos Fortes:** Captura o **significado** e a **intenção**, permitindo a recuperação de documentos semanticamente relevantes, mesmo que não compartilhem nenhuma palavra-chave com a consulta.
    
- **Fraqueza:** Mais lenta, computacionalmente intensiva e pode ser "difusa" demais, às vezes perdendo resultados onde a correspondência exata de uma palavra-chave era crucial.
    

#### 3. Metadata Filtering

- **Como Opera:** Um filtro booleano (sim/não) que restringe os resultados com base em atributos armazenados nos metadados do documento (ex: `ano > 2023`, `autor == "João"`).
    
- **Pontos Fortes:** Rápido, interpretável e aplica regras de negócio rígidas que as outras duas técnicas não conseguem.
    
- **Papel:** Não é uma técnica de _recuperação_, mas sim de _restrição_.
    

---

### 2. O Pipeline da Hybrid Search

O processo de busca híbrida normalmente segue estas etapas:

1. **Consulta:** O retriever recebe o prompt do usuário.
    
2. **Execução Paralela:** O retriever executa a **Keyword Search** e a **Semantic Search** _simultaneamente_ com o mesmo prompt.
    
3. **Resultados Brutos:** Isso gera duas listas de resultados classificadas (ranqueadas) de forma independente. (Ex: 50 melhores resultados da Keyword, 50 melhores da Semântica).
    
4. **Filtragem (Opcional):** O Metadata Filtering é aplicado a _ambas_ as listas, removendo documentos que não atendem aos critérios (ex: usuário não tem permissão de acesso).
    
5. **Fusão:** As duas listas filtradas são combinadas em uma única lista final usando um algoritmo de fusão.
    

	![[Pasted image 20251031130339.png]]
---

### 3. O Algoritmo de Fusão: Reciprocal Rank Fusion (RRF)

A etapa mais crucial é a fusão. Um algoritmo comum para isso é o **Reciprocal Rank Fusion (RRF)**. O RRF é elegante porque **ignora os scores de relevância originais** (que não são comparáveis, como um score BM25 e uma similaridade de cosseno) e usa apenas a **posição (rank)** do documento em cada lista.

A fórmula do RRF para um documento `d` é:

$$Score_{RRF}(d) = \sum_{r \in Rankings} \frac{1}{k + rank_r(d)}$$

Onde:

- `rank_r(d)` é a posição (rank) do documento `d` na lista de resultados `r`.
    
- `k` é um hiperparâmetro de suavização.
    
	![[Pasted image 20251031130452.png]]
#### O Papel do Hiperparâmetro `k`

O `k` controla o impacto dos documentos de alto escalão:

- **Se $k = 0$:** O algoritmo recompensa agressivamente o primeiro lugar. Um documento em 1º lugar (`rank=1`) ganha $1/1 = 1.0$ ponto, enquanto o 10º (`rank=10`) ganha $1/10 = 0.1$ ponto (uma diferença de 10x). Um único 1º lugar pode dominar a classificação final.
    
- **Se $k > 0$ (ex: $k = 50$):** O `k` "suaviza" a curva. O 1º lugar ganha $1/51 \approx 0.0196$ pontos, e o 10º ganha $1/60 \approx 0.0166$. A diferença é muito menor, dando mais peso à consistência (um documento que aparece em 10º em ambas as listas pode pontuar mais do que um que aparece em 1º em uma e 50º em outra).
    

---

### 4. Ajuste Fino (Fine-tuning)

A força da busca híbrida está em sua capacidade de ajuste:

- **Ponderação (Beta/Alpha):** Além do RRF, é comum introduzir um hiperparâmetro de ponderação (o texto o chama de `beta`, mas `alpha` também é usado) para controlar a importância relativa de cada lista.
    
    - **Exemplo:** 70% Semântica, 30% Keyword (`beta = 0.7`).
        
    - **Caso de Uso 1 (Técnico):** Se o conteúdo é rico em nomes de produtos, pode-se aumentar o peso da Keyword Search.
        
    - **Caso de Uso 2 (Conceitual):** Se o conteúdo é sobre conceitos abstratos, aumenta-se o peso da Semantic Search.
        
- **Ajuste de `k`:** Alterar o valor `k` no RRF para recompensar mais ou menos os resultados de topo.
    
- **Ajuste de `Top_k` (pré-fusão):** Alterar quantos documentos (ex: 50) cada busca (Keyword/Semantic) recupera _antes_ da fusão.
    

### Conclusão

Após a fusão e reclassificação pelo RRF, o retriever simplesmente retorna o `Top_k` (ex: os 10 melhores) da lista híbrida final.

Esta abordagem permite que o sistema se beneficie simultaneamente da **precisão literal** da Keyword Search e da **compreensão de significado** da Semantic Search, enquanto ainda impõe **regras de negócio** através do Metadata Filtering.