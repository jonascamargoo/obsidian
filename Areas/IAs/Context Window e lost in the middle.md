---
tipo: conceito
area: IAs
tags:
- ia
criada: '2025-11-04'
---

Por que aos chatbots AI-powered se perdem ao longo da conversa? (respondido no final). Mais detalhes podem ser vistos  [[Engenharia de prompt em RAGs|aqui]].
## Mecanismo de Conversa Multi-Turn

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
    
2. A Aplicação envia esta lista inteira (3 mensagens) para a LLM.
    
3. A LLM responde "A capital é Ottawa.".
    
4. A **Aplicação** armazena o histórico atualizado: (agora com 4 mensagens).
    

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

## Voltando à pergunta: por que IAs se perdem?
#### Causa 1: O Limite da Janela de Contexto (O "Problema Difícil")

Todo modelo (Gemini, GPT-4, etc.) tem um limite máximo de tokens (a "Janela de Contexto" - ex: 32.000 tokens).

1. **Turno 1:** O histórico tem 50 tokens.
    
2. **Turno 10:** O histórico tem 2.000 tokens.
    
3. **Turno 100:** O histórico tem 31.000 tokens. Tudo funciona bem.
    
4. **Turno 101:** O histórico agora teria 32.100 tokens, o que é **maior que o limite** de 32k.
    

A aplicação (ChatGPT ou Gemini) **não pode** enviar mais tokens do que o limite. A única solução é o **Truncamento**: a aplicação começa a **deletar as mensagens mais antigas** (o Turno 1, Turno 2, etc.) do histórico para que o total (histórico antigo + nova pergunta) caiba na janela.

**Resultado:** O modelo literalmente **esquece** o que vocês discutiram no início da conversa (instruções, fatos, a premissa). Ele fica "menos inteligente" porque está operando com uma memória incompleta.

#### Causa 2: "Perdido no Meio" ou "Lost in the Middle" (O "Problema Sutil")

Este é o problema mais técnico e interessante, que acontece **mesmo que você não tenha atingido o limite** da janela de contexto.

Pesquisas sobre a arquitetura Transformer (e a $O(N^2)$ da Atenção) mostram que os modelos **não prestam atenção de forma uniforme** a um prompt longo.

Um Transformer é excelente em prestar atenção a duas coisas:

1. O **Início** do prompt (ex: o `System Prompt` ou as primeiras instruções).
    
2. O **Fim** do prompt (ex: sua pergunta mais recente).
    

Ele é notoriamente **ruim** em prestar atenção ao conteúdo que está no **meio** do prompt.

Em uma conversa longa (Turno 100), o prompt que o modelo recebe se parece com isto:

- `[INSTRUÇÕES DO SISTEMA]` **(Atenção Alta)**
    
- `[Turno 1: Usuário/Assistente]` (Meio)
    
- `[Turno 2: Usuário/Assistente]` (Meio)
    
- ...
    
- `[Turno 99: Usuário/Assistente]` (Meio)
    
- `[Turno 100: Pergunta Atual]` **(Atenção Alta)**
    

O modelo "perde" as nuances, fatos e instruções que foram estabelecidos nos turnos 10, 30 ou 90, porque essa informação está "perdida no meio" da janela de contexto. Ele responde de forma mais genérica porque não está usando o contexto específico que vocês construíram.

---

### 2. O que Fazer?

Você pode combater ativamente esses dois problemas:

1. **A Solução Mais Fácil (Hard Reset):**
    
    - **Inicie uma nova conversa.**
        
    - Isso limpa completamente o histórico, esvazia a janela de contexto e redefine o foco da atenção. É a solução mais garantida para ter o modelo 100% "inteligente" novamente.
        
2. **A Solução de Contexto (Soft Reset):**
    
    - **Relembre o modelo.**
        
    - Como sabemos que o modelo presta atenção ao **fim** do prompt, você pode "forçar" o contexto perdido de volta para a zona de atenção alta.
        
    - Comece sua pergunta com um lembrete:
        
        - "Lembre-se que definimos que X=Y no início da conversa. Agora..."
            
        - "Vamos recapitular: já estabelecemos que A, B e C. Baseado nisso..."
            
        - "Ignorando as últimas 5 mensagens, vamos voltar ao tópico de HNSW..."
            
3. **A Solução de Resumo:**
    
    - Faça um resumo dos pontos-chave da conversa até agora e cole-o em seu prompt.
        
    - Isso serve como uma forma de "compressão de contexto", substituindo o "meio" ruidoso e longo por um resumo curto no final, que o modelo _irá_ ler com atenção.


![[Pasted image 20251103232448.png]]