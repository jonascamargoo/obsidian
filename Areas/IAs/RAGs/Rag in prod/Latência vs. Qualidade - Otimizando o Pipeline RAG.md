---
tipo: conceito
area: IAs
tags:
- ia/rag
- ia/llmops
criada: '2026-02-23'
---

**Data:** 23/02/2026 **Tópico:** #BackendEngineering #Performance #Latency #RAG #SystemDesign

---

## ⚖️ 1. O Contexto dita a Tolerância

A "latência aceitável" não é um número fixo, mas depende do caso de uso:

- **E-commerce:** Exige baixíssima latência para recomendações; usuários têm pouca paciência. Aqui, sacrifica-se a "perfeição" do item pela velocidade.
    
- **Saúde/Diagnóstico:** Foca-se na qualidade máxima da resposta. O médico tolera uma espera maior por uma análise precisa de doenças raras.
    

---

## 🐢 2. Identificando os Gargalos (The Transformer Tax)

Quase toda a latência de um sistema RAG é resultado da execução de modelos baseados em **Transformers**.

- **O Vilão Principal:** Chamadas ao LLM principal (Geração).
    
- **Outros Culpados:** Rerankers baseados em Transformer, roteadores e reescritores de query.
    
- **O Ponto Rápido:** Bancos de dados vetoriais modernos são geralmente muito rápidos e escalam bem, contribuindo pouco para a latência total.
    
	![[Pasted image 20260223172609.png]]
---

## 🛠️ 3. Estratégias de Redução de Latência

### Otimização do LLM (Ponto de Partida)

- **Modelos Menores ou Quantizados:** Rodam sempre mais rápido no mesmo hardware.
    
- **Roteamento Inteligente (Router LLM):** Use um LLM pequeno para classificar a query. Queries simples vão para modelos rápidos; queries complexas vão para modelos potentes.
	![[Pasted image 20260223234902.png]]
    
- **Caching Semântico:** Mantém um cache de prompts frequentes. Se a nova query for similar a uma cacheada, retorna-se a resposta imediatamente, pulando a geração.
    
    - _Dica:_ Pode-se usar um LLM rápido para apenas ajustar levemente a resposta cacheada ao novo contexto (personalização rápida).
        

### Refinamento do Pipeline

Cada componente adicionado (reescrita de query, reranking) deve "pagar o aluguel" em termos de qualidade.

- **Métrica:** Meça a latência incremental _vs._ a melhoria na qualidade. Se um reescritor de query adiciona 500ms mas melhora a precisão em apenas 1%, considere removê-lo.
    

### Otimização da Recuperação (Retrieval)

Mesmo sendo rápida, a busca pode ser otimizada para escalas massivas:

- **Quantização Binária:** Simplifica os cálculos de distância vetorial no banco.
    
- **Sharding:** Fragmentar bancos de dados muito grandes em múltiplas instâncias para reduzir o tempo de busca.
    

---

## 📈 4. Fluxo de Trabalho do Engenheiro

1. **Defina o SLA:** Entenda quanto de latência seu projeto tolera.
    
2. **Ataque o Core LLM:** É o maior ganho potencial.
    
3. **Avalie Componentes Adjacentes:** Revise roteadores e rerankers.
    
4. **Otimize o Banco:** Use sharding e quantização binária se necessário.
    

> [!TIP] **Observabilidade é Chave** Utilize seu sistema de traces para ver o tempo exato de cada span. Isso permite identificar se o atraso está na rede, no banco de dados ou (como geralmente ocorre) no tempo de processamento dos tokens do LLM.