## 1. A Anatomia do Padrão ReAct

O padrão **ReAct** (Reasoning + Acting) é a fundação teórica da maioria dos agentes autônomos. Ele força o LLM a intercalar etapas de raciocínio (Chain of Thought) com ações no ambiente externo, resolvendo o problema de alucinação e falta de aterramento (_grounding_) de prompts diretos.

Em vez de prever a resposta final imediatamente, o LLM é instruído a operar em um ciclo estrito:

1. **Thought (Raciocínio):** O modelo planeja o próximo passo.
    
2. **Action (Ação):** O modelo seleciona uma ferramenta e seus parâmetros.
    
3. **PAUSE (Interrupção):** O LLM para de gerar tokens (cedendo controle de volta ao nosso código Python).
    
4. **Observation (Observação):** O nosso código (_runtime_) executa a ferramenta e injeta o resultado de volta no contexto do LLM.
    
5. **Answer (Síntese):** Após $N$ iterações, o modelo consolida as observações na resposta final.
    

---

## 2. Gerenciamento de Estado (A Classe `Agent`)

A construção de um agente "do zero" revela que a "inteligência" reside na orquestração do histórico de mensagens. A classe `Agent` atua como o repositório de estado (memória de curto prazo) e o cliente HTTP para a API de inferência.

```Python
class Agent:
    def __init__(self, system=""):
        self.system = system
        self.messages = [] # Buffer de memória conversacional
        if self.system:
            self.messages.append({"role": "system", "content": system})

    def __call__(self, message):
        self.messages.append({"role": "user", "content": message})
        result = self.execute()
        self.messages.append({"role": "assistant", "content": result})
        return result
```

- **A Abstração:** O método `__call__` encapsula a mutação de estado. Cada interação anexa o _input_ do usuário (ou a _Observation_ do sistema) e o _output_ do assistente de volta ao _array_ de contexto, garantindo que o LLM "lembre" dos passos anteriores da inferência.
    
- **Determinismo:** Durante o método `execute()` (onde `client.chat.completions.create` é chamado), o parâmetro `temperature=0` é crucial. Agentes precisam de estabilidade na formatação de saída para que os _parsers_ (Regex) não quebrem.
    

---

## 3. O Prompt de Sistema como um Motor de Controle

Sem APIs de _Function Calling_ nativas (como as usadas no LlamaIndex na lição anterior), o roteamento do agente depende de **Text Parsing**. O _System Prompt_ atua como o contrato de interface (API contract) para o LLM.

```markdown
You run in a loop of Thought, Action, PAUSE, Observation.
...
Your available actions are:
calculate:
e.g. calculate: 4 * 7 / 3
...
```

**Técnicas de Prompting Utilizadas:**

1. **Definição de Máquina de Estados:** Instruções explícitas sobre as palavras-chave de transição de estado (`Thought`, `Action`, `PAUSE`).
    
2. **Tool Registry Inject:** As funções Python disponíveis são descritas em texto simples (def calculate:...).
    
3. **One-Shot Example:** Fornecer um exemplo completo de _trace_ (pergunta $\rightarrow$ pensamento $\rightarrow$ ação $\rightarrow$ observação $\rightarrow$ resposta) reduz drasticamente a taxa de falha de formatação do LLM em comparação com abordagens _zero-shot_.

---

## 4. O Runtime (Event Loop e Regex Parsing)

O _runtime_ é o código que envelopa o LLM, responsável por capturar o texto, interpretá-lo como comandos executáveis e realimentar o LLM.

### Extração de Ações via Regex

Como o LLM retorna texto livre, usamos Expressões Regulares para decodificar a intenção da chamada de ferramenta:

```Python
# Captura o nome da ferramenta (Group 1) e os parâmetros (Group 2)
action_re = re.compile('^Action: (\w+): (.*)$')
```

### O Loop de Orquestração (`query`)

O "Agent Loop" é fundamentalmente um `while` iterativo limitado por `max_turns` (para evitar loops infinitos de custos de API):

1. **Inferência:** O LLM gera um bloco de texto.
    
2. **Parsing:** O Regex varre as linhas procurando por `Action: [ferramenta]: [parâmetros]`.
    
3. **Roteamento (Conditioning):**
    
    - **Se encontrou ação:** Extrai os parâmetros, busca o ponteiro da função Python no dicionário `known_actions` e executa a função localmente.
        
    - **Se NÃO encontrou ação:** Assume que o LLM chegou no estado `Answer` (conclusão) e quebra o loop (`return`).
        
4. **Feedback:** Formata o retorno da função Python (_Observation_) e o reinjeta no LLM chamando `bot(next_prompt)`.
    

> [!NOTE] Limitações desta Abordagem "Vanilla"
> 
> Esta implementação expõe a fragilidade dos agentes baseados puramente em texto. Se o LLM alucinar a sintaxe e gerar `Action -> calculate (4*7)` em vez de `Action: calculate: 4*7`, o Regex falha silenciosamente ou quebra o loop. É exatamente por isso que o mercado migrou para _Function Calling LLMs_ estritos (JSON struct) e orquestradores de estado robustos como o LangGraph.

---

### Tags & Referências

- #ReAct #AgenticArchitecture #StateMachines #PromptEngineering #RegexParsing #LLMOps #PythonRuntime
