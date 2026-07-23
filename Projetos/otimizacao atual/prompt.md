---
tipo: projeto
area: otimizacao atual
tags:
- ia/agentes
criada: '2026-04-20'
---

# Prompt para Continuidade de Refatoração: Axur Sales Copilot V2

**Objetivo:** Atuar como um Engenheiro de Software Senior para implementar o plano de otimização de performance do "Axur Sales Copilot", um sistema de RAG (Retrieval-Augmented Generation).

**Contexto da Arquitetura Atual:**

- **Core:** `CopilotService` (orquestrador principal).
    
- **Fluxo Atual (Sequencial):** Tradução -> Multi-query -> Busca Vetorial (ChromaDB) -> Workflow de Resposta (General QA ou RFP).
    
- **Gargalo Identificado:** Latência acumulada por chamadas síncronas de LLM em cascata.
    

**Plano de Ação para Implementação (Seguir estritamente):**

### 1. Unificação da Inteligência (Query Expansion)

- **Tarefa:** Substituir as chamadas de tradução e multi-query por uma única.
    
- **Alteração:** No arquivo `features/query_understanding/analyzer.py`, fundir as lógicas de `translate` e `generate_multiqueries`.
    
- **Prompt Unificado:** O novo prompt deve retornar um JSON com `detected_language`, `translated_query` e `expanded_queries`.
    

### 2. Paralelização de Busca e Análise

- **Tarefa:** Executar a análise da query e a busca no banco simultaneamente.
    
- **Alteração:** Em `core/copilot_service.py`, usar `concurrent.futures.ThreadPoolExecutor` para disparar a `query_analyzer.analyze_query_batch` ao mesmo tempo que uma busca `vectorstore.similarity_search` inicial.
    

### 3. Implementação de Resposta via Streaming

- **Tarefa:** Reduzir a latência percebida entregando tokens em tempo real.
    
- **Alteração Backend:** Mudar `execute()` em `features/general_qa/qa_workflow.py` para usar `chain.stream()`.
    
- **Alteração Frontend:** Ajustar `main.py` para consumir o gerador usando `st.write_stream`.
    
- **Desafio:** Lidar com o parse de JSON parcial durante o stream (campos `reasoning` e `answer`).
    

### 4. Re-Ranking e Redução de Contexto

- **Tarefa:** Refinar os `k=25` resultados para os 5-8 mais relevantes.
    
- **Alteração:** Em `infrastructure/vector_db/retriever.py`, integrar uma biblioteca de re-ranking local (ex: FlashRank).
    

---

**Instruções para o Chat:**

1. Eu enviarei o código dos arquivos específicos que vamos mexer agora.
    
2. Você deve sugerir a alteração mantendo a **Clean Architecture** e a **tipagem (Pydantic)** já existente no projeto.
    
3. Não altere as regras de negócio de TLP (Traffic Light Protocol) ou segurança de domínio (`check_user_is_axurian`).
    
4. **Estado Atual:** Informe em qual item do plano de ação estamos trabalhando no momento.
    

---

### Como utilizar este prompt:

1. Sempre que sentir que a IA está se perdendo, abra um novo chat.
    
2. Cole o texto acima.
    
3. Logo em seguida, cole o conteúdo do arquivo que você quer refatorar naquele momento (ex: o `copilot_service.py`).
    
4. Diga: _"Estou pronto para começar o Item X do plano de ação. Analise o arquivo enviado e sugira as mudanças."_
    

Isso garante que a IA tenha o "Norte" (o plano de ação) e o "Chão" (o código atual) sem as distrações do histórico acumulado.