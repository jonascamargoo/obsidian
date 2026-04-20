Atue como um Engenheiro de Software Sênior e Especialista em IA para me ajudar a continuar o desenvolvimento do backend de um aplicativo chamado "ismr". 

# 1. Visão Geral do Projeto (ismr)
O **ismr** é um aplicativo voltado para a "economia do movimento" (entregadores, motoristas de app, etc.). Ele roda em background no celular, escuta as notificações do SO e usa IA para ler, resumir e contextualizar essas mensagens no fone de ouvido do usuário, evitando que ele precise olhar para a tela. 
Eu estou desenvolvendo o backend (repositório: `ismr-engine-service`) e um amigo está fazendo o frontend/mobile (React/React Native).

# 2. Stack Tecnológica Atual
- **Linguagem:** Python (Sou dev Python e Machine Learning Engineer).
- **Framework Web:** FastAPI.
- **Banco de Dados:** PostgreSQL hospedado no Neon (Serverless).
- **ORM:** SQLAlchemy.
- **Validação de Dados:** Pydantic.
- **Estratégia de IA:** Utilizaremos modelos locais (Ollama rodando Llama 3 ou Mistral) via Few-Shot Prompting. Sem fine-tuning.

# 3. Estado Atual do Código (O que já está pronto)
Já temos o `main.py` configurado com a conexão ao Neon via `.env` (`psycopg2-binary` e `python-dotenv`). O banco possui a tabela `user_preference` criada via SQLAlchemy. 
Para o MVP, estamos ignorando autenticação e usando um `FIXED_USER_ID` ("00000000-0000-0000-0000-000000000001"). 

Já temos dois endpoints funcionando (CRUD básico para o frontend):
- `GET /preferences`: Retorna as preferências do usuário.
- `PUT /preferences`: Atualiza as preferências.
Os campos da tabela/schema são: `user_id`, `default_language`, `verbosity` (ex: "Contextual", "Curto"), `default_voice` e `delivery_frequency`.

# 4. Plano de Ação e Próxima Tarefa
Nossa próxima meta é criar um endpoint de simulação para o frontend testar a IA, sem precisar de toda a infraestrutura mobile rodando.

**Sua tarefa:**
Crie o código para um novo endpoint `POST /simulate-ai`. 
1. Ele deve receber um payload com o texto de uma notificação bruta (ex: "WhatsApp | João: Mano, o endereço mudou para a rua B").
2. Ele deve buscar as preferências do `FIXED_USER_ID` no banco de dados (especialmente o campo `verbosity`).
3. Ele deve montar um Prompt de Sistema (System Prompt) otimizado usando a técnica de Few-Shot Prompting, instruindo a IA sobre como ela deve processar aquele texto baseada na verbosidade escolhida pelo usuário.
4. Por enquanto, crie uma função "mock" (simulada) para a chamada da IA (que depois substituiremos pela chamada real ao Ollama) que retorne o texto transformado.

Por favor, forneça o código para esse endpoint e os schemas do Pydantic necessários para ele, mantendo o padrão em inglês.