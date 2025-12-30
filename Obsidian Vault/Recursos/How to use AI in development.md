## Workflow de Desenvolvimento Orientado a IA

### Fase 1: Preparação e Contexto

Antes de escrever código, preparamos o terreno para a IA operar com eficiência.

#### 1. Prompt em Inglês (Sempre)

- **O que é:** Utilizar a língua inglesa para interagir com o modelo, mesmo que o código final tenha comentários em PT-BR (se for regra da empresa).
    
- **Por que utilizar:** A vasta maioria do dataset de treino dos LLMs (Large Language Models) é em inglês. Prompts em inglês tendem a ter menos "alucinações" de tradução, maior precisão técnica e melhor aderência a termos da indústria.
    
- **Exemplo:**
    
    > _Ruim:_ "Crie uma função que pegue o usuário do banco." _Bom:_ "Create a function to fetch the user from the database using JPA criteria."
    

#### 2. Utilização de Git Worktree

- **O que é:** Criar cópias do repositório em pastas separadas vinculadas a _branches_ diferentes, permitindo testar abordagens isoladas rapidamente.
    
- **Por que utilizar:** A IA gera muito código rápido, e às vezes, muito código errado. O `git worktree` permite que você peça para a IA "tentar a abordagem A" em uma pasta e "tentar a abordagem B" em outra, sem sujar seu diretório de trabalho principal (`stash` ou `switch` constantes).
    
- **Exemplo:**
    
    > `git worktree add ../feature-nova-ai feature/nova-implementacao`
    

---

### Fase 2: Planejamento e Arquitetura

Aqui a IA atua como um **Arquiteto de Software**.

#### 3. Planejamento no Claude Code ("The Architect")

- **O que é:** Usar modelos com janelas de contexto grandes e raciocínio superior (como Claude 3.5 Sonnet ou Opus) para desenhar a solução _antes_ de abrir o editor de código.
    
- **Por que utilizar:** O Claude tende a ser menos "afobado" que outros modelos para escrever código. Ele é excelente para criar o esqueleto, pensar em _edge cases_ e definir a estrutura de arquivos.
    
- **Exemplo:**
    
    > "I need to implement a notification system. Create a step-by-step implementation plan considering a microservices architecture. Don't write code yet, just the strategy and file structure."
    

#### 4. Gestão de Contexto e Validação (Anti-Alucinação)

- **O que é:** Forçar o modelo a provar que entendeu o que deve ser feito (Modo "Ask" no Cursor ou chat).
    
- **Por que utilizar:** Garantir que o modelo não está ignorando regras de negócio ou inventando bibliotecas. Mesmo em sistemas com RAG (Retrieval-Augmented Generation), trazer uma referência explícita (um snippet de código existente ou documentação) ancora o modelo na realidade.
    
- **Técnica de Validação:**
    
    > "Before generating the code, explain to me your understanding of the task and list the existing project constraints based on the context provided."
    

---

### Fase 3: Execução e Refinamento

Aqui a IA atua como um **Desenvolvedor Pleno**.

#### 5. Clean-up no Cursor ("The Builder")

- **O que é:** Pegar o planejamento/esboço feito pelo Claude e usar o Cursor (ou Copilot) para implementar, refatorar e limpar o código dentro da IDE.
    
- **Por que utilizar:** O Cursor tem contexto do seu repositório local. Ele consegue ver que uma variável sugerida pelo Claude não existe no seu projeto e corrigir isso em tempo real (Apply/Diff).
    
- **Ação:** Usar o `Cmd+K` (ou atalho equivalente) para iterar sobre o código gerado: _"Refactor this function to match the coding style of the file utils.ts present in the context."_. Lembrar de colocar no modo planejamento
    

---

### Fase 4: Revisão e Qualidade (QA)

Aqui a IA atua como um **Senior Tech Lead** e **QA**.

#### 6. Persona "Senior Reviewing Junior"

- **O que é:** Pedir para a IA revisar o código gerado (por ela mesma ou por você) assumindo que o código foi escrito por um júnior.
    
- **Por que utilizar:** LLMs tendem a ser "bonzinhos" (sycophancy). Se você pede apenas "Revise", ele diz "Está ótimo!". Se você diz "Um júnior escreveu isso, encontre erros de segurança, performance e _code smells_", a IA se torna muito mais criteriosa e rigorosa.
    
- **Prompt Exemplo:**
    
    > "Act as a Senior Staff Engineer. Review the following code written by a Junior Developer. Be extremely critical regarding performance, security, and memory leaks. Don't be polite, strictly focus on code quality."
    

#### 7. Suporte Antecipado (Pre-mortem)

- **O que é:** Usar a LLM para prever dúvidas de QAs (Quality Assurance) ou de usuários não técnicos.
    
- **Por que utilizar:** Reduz o vaivém de tickets e suporte interno. Você blinda o código contra perguntas óbvias criando respostas ou melhorando a usabilidade antes do lançamento.
    
- **Exemplo:**
    
    > "Analyze this feature from a generic user's perspective. What are the top 3 questions or errors they might encounter? Write a troubleshooting guide for them."
    

---

### Fase 5: Entrega

Aqui a IA atua como **Documentador**.

#### 8. Escrever o Próprio Pull Request (PR)

- **O que é:** Eu escrever meu próprio Pull Request.
    
- **Por que utilizar:** Se eu não conseguir explicar o porquê estou subindo algo ou porque fiz tal alteração, é um alerta de que deleguei muita tarefa para a IA
    
- **Ferramenta:** Funcionalidade nativa do Cursor ou via CLI com IA.
    

---

### Consideração Final: Padrões Agnósticos a LLM

- **Dúvida:** "Não sei se devo usar padrões agnósticos."
    
- **Veredito:** **Sim, você deve.**
    
- **Por que:** Os modelos mudam toda semana (GPT-4, Claude 3.5, Llama 3). Se você criar um fluxo de trabalho que depende _exclusivamente_ de um "hack" de prompt que só funciona no GPT-4, seu processo quebra quando você mudar para o Claude.
    
- **Como aplicar:** Foque em princípios de Engenharia de Software (SOLID, Clean Code) e use a IA para aplicar esses padrões universais, em vez de pedir "escreva código do jeito que o GPT gosta". Código limpo é código limpo para qualquer IA.