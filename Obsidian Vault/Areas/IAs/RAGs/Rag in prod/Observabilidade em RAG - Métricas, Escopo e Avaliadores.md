**Data:** 23/02/2026

**Tópico:** #SRE #LLMOps #RAG #Observability #SoftwareEngineering

---

## 🏗️ Arquitetura do Sistema de Observabilidade

Um sistema de observabilidade para RAG não deve apenas monitorar logs, mas sim cruzar performance de software com a qualidade semântica das saídas.

### 1. Telemetria e Logs

- **Métricas de Performance (Standard SW Metrics):** Latência ($p50, p95, p99$), throughput (RPS), consumo de memória/CPU e **Tokens per Second (TPS)**.
    
- **Estatísticas Agregadas:** Essenciais para identificar regressões após novos deploys.
    
- **Distributed Tracing:** Logs detalhados que permitem rastrear a "jornada do prompt" através de todos os nós do pipeline (Retrieval -> Augmentation -> Generation).
    

### 2. Capacidade de Experimentação

O sistema deve suportar **A/B Testing** e **Shadow Deployments** para validar:

- Troca de Modelos (ex: GPT-4o vs. Claude 3.5).
    
- Ajustes no _System Prompt_.
    
- Tuning de hiperparâmetros do Retriever (ex: $k$ vizinhos, algoritmos de reranking).
    

---

## 🗺️ Matriz de Avaliação (Framework Scope x Type)

A avaliação é dividida em duas dimensões principais: **Escopo** e **Tipo de Avaliador**.

### A. Dimensão: Escopo (Scope)

|**Nível**|**Descrição**|**Exemplo de Uso**|
|---|---|---|
|**System-level**|Visão holística do pipeline.|Avaliar se a resposta final satisfez o usuário.|
|**Component-level**|Isolamento de módulos (Retriever, Generator).|Identificar se a latência alta vem do Vector DB ou da inferência do LLM.|

### B. Dimensão: Tipo de Avaliador (Evaluator Type)

1. **Code-based (Deterministic):**
    
    - **Prós:** Barato, rápido, determinístico, integrável ao CI/CD.
        
    - **Exemplos:** Unit tests para saídas JSON, contagem de tokens, verificação de regex.
        
2. **Human-in-the-loop (HITL):**
    
    - **Prós:** "Ground truth" real; captura nuances que o código ignora.
        
    - **Contras:** Caro, lento, difícil de escalar.
        
    - **Exemplos:** Thumbs up/down, feedback qualitativo, curadoria de datasets de teste (Golden Sets).
        
3. **LLM as a Judge:**
    
    - **Prós:** Flexível, escala melhor que humanos, mais barato que especialistas.
        
    - **Contras:** Sujeito a **Self-preference bias** (modelos tendem a dar notas maiores para respostas de sua própria família) e inconsistência em escalas contínuas (0-100).
        
    - **Best Practice:** Usar rubricas discretas (ex: "Relevante" vs "Irrelevante").
        

---

## 📊 Métricas de Qualidade Específicas para RAG

Para uma análise profunda, utilizamos bibliotecas como a **Ragas** para medir o "RAG Triad":

- **Retriever Quality:**
    
    - **Recall:** O contexto recuperado contém a resposta?
        
    - **Precision:** Quão focado é o contexto (evitando ruído)?
        
- **Generator Quality:**
    
    - **Faithfulness (Fidelidade):** A resposta é derivada exclusivamente do contexto recuperado (evita alucinação)?
        
    - **Answer Relevancy:** A resposta realmente endereça o prompt do usuário?
        
    - **Citation Quality:** As referências aos documentos originais estão corretas?
        

---

> [!TIP] **Engenharia de Confiabilidade**
> 
> Como engenheiro, foque em automatizar os **Code-based evals** no seu pipeline de deploy e utilize **LLM as a Judge** em batches assíncronos para monitorar o desvio de qualidade (drift) em produção sem onerar a latência do usuário final.