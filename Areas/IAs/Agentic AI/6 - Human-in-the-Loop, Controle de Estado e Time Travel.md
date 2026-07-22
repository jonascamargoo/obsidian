## 1. O Padrão Human-in-the-Loop (HITL)

Em aplicações agentic corporativas, agentes autônomos raramente têm permissão irrestrita para executar ações que modificam estado no mundo real (como `DROP TABLE`, enviar um e-mail ou fazer uma compra). O padrão _Human-in-the-Loop_ introduz uma aprovação manual e síncrona no meio de um fluxo assíncrono.

### O Redutor de Estado Personalizado (`reduce_messages`)

Para suportar edição humana, a memória do agente precisa permitir substituição, não apenas acréscimo.

- **O Problema do `operator.add`:** Em aulas anteriores, o estado `messages` apenas acumulava (append) novos eventos. Se um humano tentasse corrigir uma mensagem, ela seria duplicada.
    
- **A Solução:** Implementa-se uma função `reduce_messages` que avalia os IDs (UUIDs) das mensagens. Se um ID já existir no grafo, a mensagem é **substituída** (Update). Se não existir, ela é **anexada** (Append).
    

### O Mecanismo de Interrupção (`interrupt_before`)

A interrupção é injetada na camada de compilação do LangGraph, definindo uma barreira arquitetural:

```Python
self.graph = graph.compile(
    checkpointer=checkpointer,
    interrupt_before=["action"] # Para a execução ANTES de invocar qualquer ferramenta
)
```

**Fluxo de Execução:**

1. O usuário envia a query $\rightarrow$ O grafo entra no nó `LLM`.
    
2. O `LLM` decide chamar uma ferramenta (ex: _Search LA_).
    
3. O LangGraph avalia o próximo nó. É o `action`. Como há uma regra `interrupt_before`, a execução é congelada e o controle retorna para a thread principal (para o código Python/interface).
    
4. O humano aprova $\rightarrow$ O fluxo é retomado invocando `graph.stream(None, thread)`. O `None` indica que não há novo input, o grafo deve apenas continuar de onde parou.
    

---

## 2. Manipulação de Estado em Tempo de Execução (Steerability)

Além de aprovar ou negar, a verdadeira utilidade do HITL é a capacidade de "corrigir a rota" (_Steering_) do agente quando ele alucina ou toma uma decisão subótima.

### Corrigindo a Intenção do Agente

Se o agente decidir buscar _"Clima em LA"_ mas você quiser _"Clima na Louisiana"_:

1. Lemos o estado atual que está pendente no checkpoint: `current_values = graph.get_state(thread)`.
    
2. Navegamos até o payload gerado pelo LLM (`tool_calls`).
    
3. Mutamos os argumentos localmente no Python: `args: {'query': 'Louisiana'}`.
    
4. Comitamos a alteração no banco de dados do Checkpointer:
    

```Python
abot.graph.update_state(thread, current_values.values)
```

Após o _update_, se retomarmos o grafo (`stream(None, thread)`), o nó `action` usará o payload corrigido pelo humano.

---

## 3. Time Travel e Versionamento de Estado

A arquitetura do LangGraph salva o estado após _cada_ transição de nó, construindo um log imutável de eventos (similar ao Git). Isso permite o padrão **Time Travel** (Viagem no Tempo).

### Conceitos Críticos de Versionamento

- `thread_id`: O identificador da conversa inteira.
    
- `thread_ts` (Timestamp): O hash/ID único de um _Snapshot_ (estado congelado) dentro daquela conversa.
    

Ao iterar sobre `graph.get_state_history(thread)`, obtemos o histórico inverso (do mais recente para o mais antigo).

### Operação de Replay (Forking da Conversa)

Se o agente chegou em uma resposta final errada após 10 passos, podemos voltar ao passo 2 e tentar outro caminho:

```Python
# 1. Recuperamos um snapshot antigo (Ex: a primeira vez que o LLM respondeu)
to_replay = states[-3]

# 2. Invocamos o grafo passando o config do snapshot antigo em vez da thread atual
graph.stream(None, to_replay.config)
```

**A Engenharia por trás do Replay:** Isso não apaga o futuro. O LangGraph cria uma "ramificação" (_Branch_), gerando novos _snapshots_ a partir daquele ponto. O estado pai (`parent_config`) das novas execuções apontará para `to_replay`.

---

## 4. Injeção de Mock Data (`as_node`)

O padrão mais avançado de manipulação permite que o humano **se passe por um nó**.

Se um LLM decidir chamar uma API cara ou perigosa, o desenvolvedor pode "falsificar" a resposta e ejetar o nó de Ação da cadeia de execução.

```Python
state_update = {"messages": [ToolMessage(
    tool_call_id=_id,
    name="tavily_search_results_json",
    content="54 degree celcius", # Human mock data
)]}

# A propriedade as_node="action" engana o orquestrador
branch_and_add = graph.update_state(to_replay.config, state_update, as_node="action")
```

**Como isso afeta o Roteamento?**

Se apenas chamarmos `update_state()`, o LangGraph pensaria: _"Ok, atualizei a memória, agora vou para o nó Action como planejado"_.

Ao usar `as_node="action"`, estamos dizendo ao orquestrador: _"Eu acabei de escrever isso NO LUGAR do nó Action. A ação já foi feita. Calcule a próxima aresta com base nisso"_.

A máquina de estados então avalia a aresta de retorno e vai direto para o nó `LLM`, evitando a execução real da ferramenta.

---

### Tags & Referências

- #LangGraph #HumanInTheLoop #TimeTravel #StateMutation #Checkpointer #LLMOps #AgenticDesign #StateGraph