---
tipo: conceito
area: IAs
tags:
- ia/rag
- ia/agentes
criada: '2026-04-20'
---

## 1. De Naive RAG para Agentic RAG

O paradigma tradicional de RAG (**Naive RAG**) opera de forma linear e síncrona: `Retrieval -> Augment -> Generation`. Embora eficiente para consultas pontuais em datasets reduzidos, essa abordagem falha em tarefas de pesquisa complexas que exigem síntese multietapa ou cruzamento de informações latentes entre documentos.

### Limitações do RAG Padrão

- **Linearidade:** O fluxo é unidirecional. Se o retrieval inicial falha ou é incompleto, a resposta final é comprometida.
    
- **Falta de Raciocínio (Reasoning):** O LLM atua apenas como um sintetizador de contexto injetado, sem capacidade de decidir se precisa de mais dados.
    
- **Escalabilidade Hierárquica:** Dificuldade em lidar com grandes volumes de documentos onde a resposta exige agregação de temas (ex: "Quais as tendências comuns nestes 20 papers?").
    

### O Paradigma Agentic

O **Agentic RAG** evolui o sistema para um framework autônomo. O agente não apenas consulta dados, mas utiliza o LLM como um motor de raciocínio para orquestrar ferramentas, gerenciar estado e decidir o fluxo de execução dinamicamente.

---

## 2. Componentes de Raciocínio (Reasoning Ingredients)

A construção de um agente de pesquisa robusto é decomposta em uma progressão de capacidades técnicas:

### A. Roteamento (Routing)

O primeiro nível de decisão. O roteador utiliza o LLM para classificar a intenção da query e direcioná-la ao "tool" ou índice de dados mais adequado.

- **Exemplo técnico:** Direcionar uma query de "resumo global" para um _Summary Index_ e uma query de "fato específico" para um _Vector Store Index_.
    

### B. Uso de Ferramentas (Tool Use)

Diferente de uma simples chamada de função, aqui o agente deve:

1. **Selecionar a ferramenta** apropriada em um inventário (interfaces).
    
2. **Gerar os argumentos** necessários (JSON schema) para a execução da ferramenta com base no contexto da query.
    

### C. Raciocínio Multietapa (Multi-step Reasoning)

Implementação de loops de pensamento (Chain of Thought / ReAct). O agente mantém uma **Memória de Curto Prazo** (contexto da conversa) e um **Estado de Execução** para:

- Decompor uma tarefa complexa em sub-tarefas.
    
- Avaliar se a saída de uma ferramenta é suficiente ou se requer nova busca.
    
- Reter informações de passos anteriores para informar decisões futuras.
    

---

## 3. Controle, Observabilidade e HITL

Para engenheiros de ML/Software, a "caixa-preta" de um agente autônomo representa um risco de produção. O curso enfatiza estratégias de governança:

### Debuggability e Rastreabilidade

- **Stepping through:** Capacidade de inspecionar o log de pensamentos (_thought process_) do agente.
    
- **Análise de Decisão:** Identificar onde o agente desviou do caminho ótimo (ex: seleção de ferramenta errada ou argumentos mal formados).
    

### Human-in-the-loop (HITL)

A inserção de guidance humano em etapas intermediárias atua como um mecanismo de **active learning** e controle de qualidade.

- **O conceito do "Manager":** O usuário atua como um gestor sênior, corrigindo o curso do agente ("busque no documento B em vez do A") para otimizar a performance sem precisar reiniciar o processo. Isso é crucial em fluxos de pesquisa de longa duração onde o custo de API e o drift de contexto são altos.
    

---

## 4. Roadmap de Implementação (LlamaIndex)

A progressão prática do curso seguirá a seguinte estrutura de construção:

1. **Router Query Engine:** Implementação sobre um único documento para lidar com QA e sumarização.
    
2. **Tool Abstraction:** Criação de interfaces para o agente interagir com APIs e índices.
    
3. **Agentic Loop:** Integração de memória e raciocínio iterativo.
    

---

### Conceitos Chave para Glossário (Obsidian Tags)

- #AgenticRAG #LlamaIndex #ReasoningLoops #ToolUse #HITL #VectorSearch #Orchestration
    

> [!IMPORTANT] **Diferença Crucial:** Enquanto o RAG comum é um **Pipeline** (estático), o Agentic RAG é um **Workflow** (dinâmico/estocástico). A complexidade migra da indexação para a orquestração de estado e prompts de raciocínio.