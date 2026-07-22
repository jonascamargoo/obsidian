Com base na arquitetura atual do **Axur Sales Copilot**, este plano de ação detalha a implementação técnica das três otimizações de maior impacto para reduzir a latência: a unificação de prompts, a paralelização da busca e a implementação de streaming.

### Fase 1: Unificação da Inteligência (Query Expansion)

O objetivo é eliminar múltiplas chamadas sequenciais à API da OpenAI no início do processo.

- **Prompt Unificado**: Criar o prompt `QUERY_EXPANSION_UNIFIED` em `shared/prompts.py`. Ele deve instruir o modelo `gpt-4o-mini` a retornar um JSON contendo a tradução e as 10 variações de busca de uma só vez.
    
- **Refatoração do Analyzer**: No ficheiro `features/query_understanding/analyzer.py`, substituir os métodos `translate` e `generate_multiqueries` por um único método `analyze_query_batch`.
    
- **Vantagem**: Redução imediata de ~3 a 5 segundos de latência de rede (round-trip).
    

### Fase 2: Paralelização e Busca Especulativa

Mudar o fluxo de linear para concorrente para que o banco de dados e a LLM trabalhem ao mesmo tempo.

- **Execução Concorrente**: No ficheiro `core/copilot_service.py`, dentro do método `get_answer`, utilizar `ThreadPoolExecutor` para disparar simultaneamente:
    
    1. A análise unificada da query (Fase 1).
        
    2. Uma busca vetorial inicial no ChromaDB usando a pergunta original do utilizador.
        
- **Lógica de Refinamento**: Se a análise da query (Fase 1) trouxer termos muito distintos da busca inicial, o `document_retriever` pode disparar uma busca complementar em background.
    
- **Vantagem**: O tempo de resposta do banco de dados (ChromaDB) é "escondido" pelo tempo de processamento da LLM.
    

### Fase 3: Resposta via Streaming (Latência Percebida)

Alterar a forma como a resposta é entregue para que o utilizador não fique a olhar para um ícone de carregamento.

- **Backend (Workflows)**: Alterar o método `execute` em `features/general_qa/qa_workflow.py` e `features/rfp_processing/rfp_qa_workflow.py` para utilizar `chain.stream()` em vez de `chain.invoke()`.
    
- **Tratamento de JSON**: Como as respostas atuais são encapsuladas em JSON (com `reasoning` e `answer`), será necessário utilizar um `OutputParser` que suporte fragmentos de JSON ou enviar o `reasoning` primeiro e depois fazer o stream apenas do campo `final_answer`.
    
- **Frontend (Streamlit)**: No ficheiro `main.py`, substituir a exibição estática por `st.write_stream` para renderizar os tokens em tempo real.
    
- **Vantagem**: O utilizador começa a ler a resposta em menos de 2 segundos, transformando a percepção de performance do sistema.
    

### Fase 4: Re-Ranking e Redução de Contexto

Otimizar o volume de dados enviado para a LLM final (`gpt-4.1`).

- **Integração de Re-Ranker**: No `infrastructure/vector_db/retriever.py`, adicionar uma camada de re-ranking (ex: FlashRank) após a recuperação inicial de `k=25`.
    
- **Filtragem de Contexto**: Reduzir os 25 documentos para os 5-8 mais relevantes antes de montar o prompt final.
    
- **Vantagem**: Reduz o custo e aumenta a velocidade da geração final, pois a LLM processa menos tokens de entrada.