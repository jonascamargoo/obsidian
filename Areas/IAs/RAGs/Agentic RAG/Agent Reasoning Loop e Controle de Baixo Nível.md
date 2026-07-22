---
tipo: conceito
area: IAs
tags:
- ia/rag
- ia/agentes
criada: '2026-04-20'
---

Para garantir escalabilidade e separação de responsabilidades, o LlamaIndex divide a entidade "Agente" em dois componentes fundamentais:

### A. Agent Worker (O Cérebro / Motor de Decisão)

Responsável por executar um **único passo** lógico.
![[Pasted image 20260416161043.png]]
- Recebe o histórico da conversa, a memória e o input atual.
    
- Utiliza o _Function Calling_ nativo do LLM para decidir: "Qual é a próxima ferramenta a ser chamada?" ou "Tenho informações suficientes para gerar a resposta final?".
    
- **Implementação:** `FunctionCallingAgentWorker`.
    

### B. Agent Runner (O Orquestrador / Event Loop)

Responsável pelo roteamento e gerenciamento de estado.

- Atua como um _Task Dispatcher_. Ele cria a tarefa (`Task`), orquestra múltiplas chamadas ao `Agent Worker` em um loop (ou fila assíncrona) e gerencia a memória.
    
- Retorna a resposta final ao usuário quando o _Worker_ sinaliza o fim da execução.
    


```Python
from llama_index.core.agent import FunctionCallingAgentWorker, AgentRunner

# Instanciação Desacoplada
agent_worker = FunctionCallingAgentWorker.from_tools(
    [vector_tool, summary_tool], 
    llm=llm, 
    verbose=True
)
agent = AgentRunner(agent_worker)
```

---

## 3. Gerenciamento de Estado (Memória Conversacional)

O framework oferece duas interfaces de alto nível com comportamentos de estado distintos:
![[Pasted image 20260416161334.png]]
- **`agent.query(prompt)`:** Execução _Stateless_. Pode realizar múltiplos passos (usar várias ferramentas para uma mesma query complexa), mas esquece o contexto após retornar a resposta final.
    
- **`agent.chat(prompt)`:** Execução _Stateful_. O `AgentRunner` mantém um buffer de memória conversacional (geralmente um _rolling buffer_ limitado à janela de contexto do LLM).
    
    - _Prova de Conceito:_ Ao perguntar "Quais os datasets de avaliação?" e, em seguida, "Me dê os resultados do _primeiro dataset mencionado_", o agente precisa recuperar o estado anterior da memória para resolver a referência cruzada, inferir o nome do dataset e montar os argumentos para o `vector_tool`.
        

---

## 4. API de Baixo Nível: Stepping e Debuggability

Em ambientes de produção (_LLMOps_), interagir com um agente apenas via `.chat()` é arriscado (caixa-preta). A arquitetura permite controle granular da execução matemática do grafo de tarefas.

### O Ciclo de Vida de uma Tarefa (Task)

Em vez de executar a query de uma vez, criamos um objeto de estado isolado:

```Python
task = agent.create_task("Tell me about the roles, and how they communicate.")
# Retorna um task_id único para rastreabilidade
```

### Inspeção e Execução Passo a Passo (_Stepping_)

O engenheiro pode iterar manualmente sobre o _Worker_:

```Python
# Executa exatamente UM ciclo de raciocínio (ex: chama apenas o summary_tool para a primeira parte da query)
step_output = agent.run_step(task.task_id)

# Observabilidade: Validação de estado
completed = agent.get_completed_steps(task.task_id)
upcoming = agent.get_upcoming_steps(task.task_id) # Útil para prever alucinações antes de gastar computação
```

### Injeção de Estado / Human-in-the-loop (HITL)

A característica mais poderosa da API de baixo nível é a **Steerability** (Dirigibilidade). O engenheiro (ou usuário, via interface assíncrona) pode injetar _prompts_ no meio da execução de uma tarefa, alterando o curso lógico do agente sem precisar reiniciar o processo.

```Python
# Injetando uma correção/nudge durante o loop:
step_output = agent.run_step(
    task.task_id, 
    input="What about how agents share information?" # Altera o CoT atual
)
```

### Finalização Segura

O loop termina quando a propriedade lógica `.is_last` do `step_output` retorna `True`. O orquestrador então consolida os resultados:

```Python
if step_output.is_last:
    response = agent.finalize_response(task.task_id)
```

> [!NOTE] Design Pattern para UX Esta arquitetura orientada a eventos (`create_task` -> loop de `run_step` -> `finalize`) é a fundação para construir interfaces assíncronas (como WebSockets) onde o usuário pode aprovar ou rejeitar o uso de uma ferramenta no meio da execução (ex: "O agente quer executar uma query SQL com DROP. Permitir? [S/N]").

---

### Tags & Referências

- #AgenticRAG #ReasoningLoop #Orchestration #StateManagement #HITL #LLMOps #ChainOfThought #LlamaIndex