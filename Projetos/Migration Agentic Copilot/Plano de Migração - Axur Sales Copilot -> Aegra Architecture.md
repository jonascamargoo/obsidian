---
tipo: projeto
area: Migration Agentic Copilot
tags:
- ia/agentes
criada: '2026-03-17'
---

## FASE 1: Preparação da Infraestrutura Base (Backend)

**Objetivo:** Abandonar a execução local em memória acoplada ao Streamlit e estabelecer o motor FastAPI com banco de dados para persistência de estado.

- [ ] **1.1. Setup do Repositório Base:**
    
    - Clone a pasta `agents/` (o backend do Aegra) para um novo diretório chamado `sales-copilot-backend`.
        
    - Mantenha a estrutura central (`src/agent_server/`, `alembic/`, `scripts/`).
        
- [ ] **1.2. Configuração do Banco de Dados (PostgreSQL):**
    
    - Suba o contêiner do PostgreSQL usando o `docker-compose.yml` fornecido pelo Aegra.
        
    - Rode as migrações iniciais para criar as tabelas de `threads`, `runs` e `checkpoints`: `python3 scripts/migrate.py upgrade`.
        
- [ ] **1.3. Limpeza do Backend Aegra:**
    
    - Na pasta `graphs/`, remova os grafos de exemplo (`scunna_agent`, `axur_agent`, `axur_bot`) para não poluir o seu projeto.
        
    - Crie uma nova pasta: `graphs/sales_copilot_agent/`.
        
- [ ] **1.4. Migração de Variáveis de Ambiente:**
    
    - Copie as variáveis de ambiente do seu projeto antigo (OpenAI, Cognito) para o novo `.env` do Aegra.
        
    - Adicione as variáveis do banco de dados (Postgres) e do Langfuse (se for usar agora).
        

## FASE 2: Migração das Regras de Negócio (RAG para "Tools")

**Objetivo:** Pegar as suas classes perfeitas de RAG (`DocumentRetriever`, Workflows) e transformá-las em ferramentas (Tools) ou funções que o LangGraph possa consumir.

- [ ] **2.1. Portabilidade da Infraestrutura de RAG:**
    
    - Copie suas pastas `infrastructure/vector_db/` (com o `retriever.py`), `core/config.py` e `shared/` para dentro do novo backend.
        
    - Garanta que o `DocumentRetriever` consiga se conectar ao ChromaDB no novo diretório.
        
- [ ] **2.2. Criação das Ferramentas (Tools) do Agente:**
    
    - Crie um arquivo `graphs/sales_copilot_agent/tools.py`.
        
    - Transforme a função que atualiza a base (`refresh_google_workspace_vectorstore`, `refresh_api_docs_vectorstore`) em `@tool` do LangChain. Exemplo: `@tool("atualizar_base_conhecimento") def sync_gws_knowledge()...`.
        
    - Transforme a busca na base (`DocumentRetriever`) em uma ferramenta invocável pelo agente (ex: `@tool("buscar_documentacao_vendas")`).
        
- [ ] **2.3. Adaptação dos Workflows (Opcional, mas recomendado):**
    
    - O seu `GeneralQAWorkflow` e `RfpQaWorkflow` são ótimos. Você pode mantê-los como funções puras que os nós (nodes) do LangGraph vão chamar quando precisarem gerar a resposta final a partir dos documentos recuperados.
        

## FASE 3: Construção do Cérebro (O Grafo LangGraph)

**Objetivo:** Substituir as instruções `if/else` gigantes do `CopilotService` (`if answer_type == "RFP": ...`) por um grafo de estados dinâmico.

- [ ] **3.1. Definição do Estado (State):**
    
    - Crie o arquivo `graphs/sales_copilot_agent/graph.py`.
        
    - Defina a classe `CopilotState(TypedDict)` ou `MessagesState`. Ela deve conter:
        
        - `messages` (lista de mensagens do LangChain).
            
        - `current_file_id` (para saber se o usuário fez upload de uma planilha de RFP).
            
        - `detected_intent` (string: "rfp", "qa_geral", "chitchat").
            
- [ ] **3.2. Criação dos Nós (Nodes):**
    
    - **Node `Router`:** Analisa a última mensagem do usuário e decide para qual nó enviar (usando a sua classe `QueryAnalyzer`).
        
    - **Node `General_QA_Agent`:** Usa a ferramenta de busca (`DocumentRetriever`) e responde perguntas comuns.
        
    - **Node `RFP_Agent`:** Focado em lidar com planilhas e checagem de Ground Truth (o fluxo do seu `RfpSpreadsheetWorkflow`).
        
- [ ] **3.3. Criação das Arestas (Edges) e Compilação:**
    
    - Conecte o Grafo: `START -> Router`.
        
    - Crie arestas condicionais: Se a intenção for RFP, vá para `RFP_Agent`; se for QA, vá para `General_QA_Agent`.
        
    - Ambos convergem para o `END`.
        
    - _Checkpointer:_ Compile o grafo passando o `MemorySaver` (ou o Checkpointer do Postgres integrado ao Aegra) para ter memória persistente.
        

## FASE 4: Integração com a API (Aegra Server)

**Objetivo:** Expor o seu novo Grafo do Copilot através dos endpoints REST padronizados (`/threads`, `/runs`).

- [ ] **4.1. Configuração do `aegra.json`:**
    
    - Abra o `aegra.json` na raiz do backend.
        
    - Altere para apontar para o seu grafo: `"sales_copilot": "./graphs/sales_copilot_agent/graph.py:graph"`.
        
- [ ] **4.2. Migração da Autenticação Cognito:**
    
    - Vá até a pasta `src/agent_server/core/`.
        
    - Injete a lógica da sua classe atual `CognitoAuthProvider` no arquivo `auth.py` ou `auth_middleware.py` do Aegra.
        
    - Isso garantirá que as rotas da API FastAPI exijam o token JWT válido do Cognito (exatamente como você fazia no Streamlit, mas agora em nível de API).
        
- [ ] **4.3. Testes de API (Postman/Curl):**
    
    - Suba o servidor (`docker compose up aegra`).
        
    - Crie uma _Thread_ (via POST `/threads`).
        
    - Envie uma mensagem e execute um _Run_ (via POST `/runs/stream`) para testar se o grafo está processando e retornando _Server-Sent Events_ (SSE).
        

## FASE 5: Substituição do Frontend (Next.js Deepagents UI)

**Objetivo:** "Jogar fora" o `main.py` do Streamlit e subir a nova interface profissional em React.

- [ ] **5.1. Setup do Frontend:**
    
    - Copie a pasta `command-master/ui/` para `sales-copilot-ui`.
        
    - Rode `yarn install`.
        
- [ ] **5.2. Personalização (White-label):**
    
    - Altere `tailwind.config.mjs` para refletir as cores da Axur (`primary: '#FF5824'`).
        
    - Substitua as logos em `public/` (como `axur_logo_.png`).
        
    - Edite os textos e títulos no `page.tsx` para "Axur Sales Copilot".
        
- [ ] **5.3. Conexão UI ↔ API:**
    
    - Configure o `.env.local` do Next.js:
        
        - `NEXT_PUBLIC_API_URL=http://localhost:8000` (URL do Aegra FastAPI).
            
        - `NEXT_PUBLIC_ASSISTANT_ID=sales_copilot` (O nome que você colocou no `aegra.json`).
            
- [ ] **5.4. Lógica de Upload de Planilhas (RFP):**
    
    - O Next.js da Deepagents já possui suporte a visualização de arquivos do agente (`FileViewDialog.tsx` e `TasksFilesSidebar.tsx`).
        
    - Adapte a barra de chat ou adicione um botão dedicado para "Fazer Upload de RFP", enviando o arquivo via API para o estado (State) do LangGraph.
        

## FASE 6: Observabilidade e Otimizações Finais

**Objetivo:** Garantir que custos, tokens e erros sejam monitorados sem poluir o código.

- [ ] **6.1. Ativar Langfuse:**
    
    - Crie uma conta/projeto no Langfuse.
        
    - Adicione as variáveis `LANGFUSE_SECRET_KEY`, `LANGFUSE_PUBLIC_KEY` e `LANGFUSE_HOST` no `.env` do backend Aegra.
        
    - O Aegra já injetará automaticamente as métricas de cada execução dos nós do seu LangGraph (você pode aposentar a sua classe `CostCalculator`).
        
- [ ] **6.2. Limpeza de Código Legado:**
    
    - Delete o `ChatMemory` baseado em S3 (pois o Postgres do Aegra agora faz isso via LangGraph Checkpointers).
        
    - Delete os cálculos manuais de tokens (`TokenCounter`).
        
- [ ] **6.3. Testes Finais e Deploy:**
    
    - Teste o "Debug Mode" na interface Next.js (rodando o agente passo a passo).
        
    - Faça o deploy do backend (FastAPI + Postgres) em um ECS/EC2.
        
    - Faça o deploy do frontend (Next.js) na Vercel ou AWS Amplify.


### Dica de Ouro para a Transição:

Não tente fazer a Fase 5 (Frontend) sem antes garantir que a Fase 3 e 4 estão perfeitas. O fluxo ideal é montar o backend, validá-lo via API/Postman e, só então, plugar a interface Next.js. Isso isola problemas visuais de problemas de roteamento do agente.


