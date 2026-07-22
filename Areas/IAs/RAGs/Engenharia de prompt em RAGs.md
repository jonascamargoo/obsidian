**Engenharia de Prompt** (Prompt Engineering) é o termo guarda-chuva para as técnicas usadas para construir prompts de alta qualidade que geram os melhores resultados de uma LLM. Em um sistema RAG, isso não envolve apenas a pergunta do usuário, mas a montagem estruturada de múltiplos componentes de informação.

---

### 1. O Padrão: O Formato `messages`

A maioria das LLMs modernas, popularizadas pela OpenAI, utiliza um formato de "mensagens" (um JSON) para estruturar a entrada. Isso é mais flexível do que uma única string.

Uma mensagem é composta por `role` (papel) e `content` (conteúdo):

- **`role: "system"`:** A mensagem do sistema. Define o comportamento, personalidade e instruções de alto nível da LLM. É a "constituição" da LLM para aquela sessão.
    
- **`role: "user"`:** A entrada do usuário (o prompt).
    
- **`role: "assistant"`:** As respostas anteriores da LLM.

    ![[Pasted image 20251103223101.png]]

---

### 2. O Mecanismo de Conversa (Multi-Turn)

O ponto mais importante a entender é que o "Mecanismo de Conversa" é, na verdade, uma **"ilusão" de memória** gerenciada pela _aplicação_ que chama a LLM, e não pela LLM em si.
#### O Problema: LLMs são "Stateless" (Sem Estado)

As LLMs são fundamentalmente **stateless**. Isso significa que cada chamada de API é um evento completamente independente e isolado. Se você faz uma chamada `API_1` perguntando "Qual a capital do Canadá?", o modelo processa e responde "Ottawa". Se você faz uma `API_2` perguntando "E do Brasil?", o modelo **não tem ideia** de que você estava falando sobre "capitais" na `API_1`. Ele vê a pergunta "E do Brasil?" isoladamente e provavelmente responderá com "O que tem o Brasil?" ou algo vago. A LLM não "se lembra" de interações passadas. Ela não mantém um "estado" de conversa.

---

#### A Solução: A Aplicação Gerencia o Estado

O "formato `messages`" (o JSON com `role` e `content`) é a solução de engenharia para esse problema. A "memória" é implementada pela _aplicação_ (o seu chatbot, o seu RAG) que, a cada novo turno, **reconstrói e reenvia o histórico completo** da conversa.

Vamos ver o fluxo técnico exato:

**Turno 1:** O usuário digita "Olá".

1. A **Aplicação** cria uma lista de mensagens:

```json
[
	{"role": "user", "content": "Olá"}
]
```

2. A Aplicação envia esta lista (1 mensagem) para a LLM.
    
3. A LLM responde "Oi! Como posso ajudar?".
    
4. A **Aplicação** agora armazena _ambas_ as mensagens:
  ```json
    [
      {"role": "user", "content": "Olá"},
      {"role": "assistant", "content": "Oi! Como posso ajudar?"}
    ]
```

**Turno 2:** O usuário digita "Qual a capital do Canadá?".

1. A **Aplicação** pega o histórico armazenado e _adiciona_ a nova mensagem:

    
    ```json
    [
      {"role": "user", "content": "Olá"},
      {"role": "assistant", "content": "Oi! Como posso ajudar?"},
      {"role": "user", "content": "Qual a capital do Canadá?"}
    ]
    ```
    
1. A Aplicação envia esta lista inteira (3 mensagens) para a LLM.
    
2. A LLM responde "A capital é Ottawa.".
    
3. A **Aplicação** armazena o histórico atualizado: (agora com 4 mensagens).
    

**Turno 3:** O usuário digita "E do Brasil?".

1. A **Aplicação** pega o histórico de 4 mensagens e _adiciona_ a nova:
   
   ```json
    [
      {"role": "user", "content": "Olá"},
      {"role": "assistant", "content": "Oi! Como posso ajudar?"},
      {"role": "user", "content": "Qual a capital do Canadá?"},
      {"role": "assistant", "content": "A capital é Ottawa."},
      {"role": "user", "content": "E do Brasil?"}
    ]
```

2. A Aplicação envia esta lista inteira (5 mensagens) para a LLM.

---

#### Por que isso Funciona? (A Conexão com a Atenção do transformer)

Quando a LLM recebe essa lista longa no Turno 3, ela a processa como **uma única sequência longa de tokens**.

Graças ao **Mecanismo de Atenção**, o token "Brasil" (na última mensagem) pode "prestar atenção" (pay _attention_) aos tokens "capital" e "Canadá" de turnos anteriores. O modelo vê o contexto completo e entende que "E do Brasil?" é uma continuação da pergunta sobre "capital".

#### O "Chat Template"

Como a LLM (Transformer) só lê uma string de texto, a aplicação (ou a API) usa um **"Chat Template"** para "achatar" (flatten) essa lista JSON em uma única string. O modelo foi treinado para reconhecer tags especiais:


```json
[
  {"role": "system", "content": "Seja útil."},
  {"role": "user", "content": "Olá"}
]
```

...é transformada (achatada) em algo como:

![[Pasted image 20251103230138.png]]

É assim que o modelo, ao ler uma única string, ainda consegue diferenciar os "papéis" (roles) de quem disse o quê.

#### A Implicação de Custo

Este método é a causa direta do **custo crescente** ($O(N^2)$) das conversas. A cada turno, a sequência de entrada ($N$) fica maior, exigindo mais computação da camada de Atenção para processar o histórico _inteiro_ novamente.
    

---

### 3. O System Prompt (O "Governante" do RAG)

O `System Prompt` é onde a lógica de negócios do RAG é definida. Ele é enviado em _cada_ chamada e instrui a LLM sobre como ela deve se comportar.

- **Características:** Pode ser extremamente longo (várias páginas) e detalhado. Pode incluir metadados (ex: data atual, data de corte do conhecimento) e definir uma persona (ex: "você é intelectualmente curioso").
    
- **Instruções Críticas para RAG:** Para um sistema RAG, o `System Prompt` é onde você injeta as regras fundamentais de _grounding_ (ancoragem):
    
    - **Ancoragem:** "Responda à pergunta do usuário usando _apenas_ os documentos recuperados fornecidos."
        
    - **Relevância:** "Se os documentos não contiverem a resposta, informe que você não sabe."
        
    - **Citação:** "Sempre cite suas fontes, indicando qual documento forneceu a informação."
        

---

### 4. O Template de Prompt Aumentado (RAG)

O prompt final enviado à LLM (o "prompt aumentado") é construído usando um **template** que combina todos esses elementos em uma ordem específica e estruturada.

Um template RAG padrão segue esta estrutura:

1. **`System Prompt`:** (Função: `system`) Define as regras de comportamento e ancoragem (grounding).
    
2. **`Chat History`:** (Função: `user` e `assistant`) Uma lista de mensagens anteriores para dar contexto à conversa.
    
3. **`Retrieved Context`:** (Função: `user` - _geralmente injetado na mensagem do usuário atual_) Os N chunks recuperados (ex: Top 5) pelo retriever.
    
4. **`Current User Prompt`:** (Função: `user`) A pergunta mais recente do usuário.
    

Usar um template torna o sistema modular e facilita a experimentação (ex: alterar o `System Prompt` ou a ordem do contexto) para ver como isso impacta a qualidade da resposta final.

![[Pasted image 20251103230601.png]]


## Engenharia de Prompt Avançada em RAG

Embora um bom `System Prompt` e um template estruturado sejam a base, técnicas de engenharia de prompt mais avançadas podem ser aplicadas para otimizar o desempenho do RAG, forçando o modelo a "aprender" o formato de resposta desejado ou a "raciocinar" sobre o problema antes de responder.

---

### 1. In-Context Learning (ICL): Ensinando por Exemplo

ICL é uma técnica onde se inserem exemplos de entradas e saídas de alta qualidade diretamente no prompt. O objetivo é "ensinar" à LLM o tom, a estrutura e o tipo de resposta esperada.

- **Tipos:**
    
    - **Few-Shot Learning:** Inserção de múltiplos exemplos (ex: 3-5).
        ![[Pasted image 20251103231516.png]]
    - **One-Shot Learning:** Inserção de um único exemplo.
        
- **Implementação em RAG:**
    
    1. **Hard-coded:** Os exemplos são estáticos e inseridos no template do prompt. Útil para comportamentos estáveis.
        
    2. **Recuperação Dinâmica (RAG-style):** Esta é uma aplicação avançada do RAG. Em vez de recuperar _fatos_, você recupera _exemplos_. A base de conhecimento é indexada com pares de (pergunta, resposta ideal) de interações anteriores (ex: chats de sucesso de atendimento ao cliente). Quando uma nova consulta chega, o RAG recupera os exemplos de conversas _mais relevantes_ para a consulta atual e os injeta no prompt.
        ![[Pasted image 20251103231555.png]]

---

### 2. Prompting Orientado ao Raciocínio (Modelos Clássicos)

Este conjunto de técnicas força a LLM a decompor um problema antes de gerar a resposta final, melhorando a precisão e fornecendo rastreabilidade.

- [**Chain-of-Thought (CoT](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FIAs%2FEngenharia%20de%20prompt%2FChain-of-Thought%20Prompting)):** A instrução "pense passo a passo" (think step-by-step). A LLM é instruída a primeiro gerar os passos lógicos necessários para responder e, em seguida, seguir esses passos para formular a resposta.
    
- **Scratchpad (Bloco de Notas):** Uma formalização do CoT. O prompt instrui a LLM a usar tags especiais (ex: `<scratchpad>...</scratchpad>`) para seu "raciocínio". A aplicação pode então exibir ou ocultar esse bloco de notas do usuário final.
    ![[Pasted image 20251103231843.png]]

**Benefícios:** Aumenta a precisão em tarefas complexas e permite a depuração (debug), pois o "trabalho" (o raciocínio) da LLM é explícito.

---

### 3. Modelos de Raciocínio (Reasoning Models)

São LLMs mais recentes projetadas "de fábrica" para se destacarem em tarefas complexas (código, matemática, planejamento).

- **Mecanismo Interno:** Elas executam o CoT/Scratchpad _automaticamente_. Elas primeiro geram **"reasoning tokens"** (o plano interno) e só depois geram os **"response tokens"** (a resposta final).
    ![[Pasted image 20251103232007.png]]
- **Implicações para RAG:**
    
    - **Pró:** São melhores na avaliação de relevância dos chunks recuperados e na síntese de informações complexas de múltiplas fontes.
        
    - **Contra:** São mais lentas e caras, pois geram tokens "ocultos" de raciocínio, além da resposta.
        ![[Pasted image 20251103232101.png]]
        
- **Interação Crítica com Prompting:** Técnicas clássicas (CoT, ICL) **funcionam mal** com esses modelos:
    
    - **CoT (Falha):** Pedir para "pensar passo a passo" é redundante e pode confundir um modelo que já faz isso.
        
    - **ICL (Falha):** Os modelos podem tentar _incorporar_ os exemplos na resposta _atual_, em vez de aprender o _formato_ (eles são muito focados na tarefa).
        
    - **O que eles preferem:** Instruções de alto nível, objetivos claros, formatos de saída específicos e o "context dump" completo (os chunks recuperados) para que possam raciocinar sobre eles.
        ![[Pasted image 20251103232322.png]]

---

### 4. O Custo: Gerenciamento da Janela de Contexto

Todas essas técnicas avançadas (ICL, CoT, RAG, histórico de chat) têm um custo direto: elas **aumentam o comprimento do prompt ($N$)**, o que eleva o custo e a latência (devido à complexidade $O(N^2)$ da Atenção).
![[Pasted image 20251103232523.png]]
Gerenciar o histórico em conversas longas (multi-turn) torna-se essencial. A solução é o **Context Pruning** (Poda de Contexto).

- **Pruning Simples (Janela Deslizante):** Manter apenas as `K` últimas mensagens.
    
- **Pruning por Resumo:** Usar uma segunda LLM (mais rápida/barata) para resumir as mensagens mais antigas, preservando o significado, mas reduzindo a contagem de tokens.
    
- **Pruning Específico de RAG:**
    
    1. **Remover Tokens de Raciocínio:** No histórico de chat, manter apenas os "response tokens" (a resposta final), descartando os "reasoning tokens".
        
    2. **Remover Contexto Antigo:** No histórico, manter apenas os chunks recuperados para a _pergunta mais recente_, descartando os chunks das perguntas anteriores.
        

### 5. Estratégia de Implementação

1. **Comece Simples:** Um bom template e um `System Prompt` claro são suficientes para a prototipagem.
    
2. **Adicione Complexidade com Validação:** Introduza técnicas avançadas (ICL, CoT, Reranking) apenas se houver uma necessidade clara e _após_ validar com métricas que elas melhoram a performance.
    
3. **Ajuste o Custo:** Gerencie ativamente a janela de contexto com estratégias de poda para equilibrar o desempenho e o custo.