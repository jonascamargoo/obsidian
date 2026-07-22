---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-11-04'
---

Avaliar um sistema RAG exige isolar seus componentes. A performance do **Retriever** (avaliada com métricas como Precision/Recall/MAP) é distinta da performance da **LLM**.

Quando se avalia a LLM, assume-se que o Retriever funcionou (ou seja, entregou documentos maioritariamente relevantes, talvez com algum ruído).

---

### 1. Isolando a Responsabilidade: O Papel da LLM

O trabalho da LLM não é _encontrar_ a informação, mas sim _usá-la_ de forma inteligente. As métricas devem focar em avaliar o quão bem ela executa estas tarefas:

1. **Síntese:** Constrói uma resposta coesa usando a informação relevante.
    
2. **Ignorar Ruído:** Resiste a ser "distraída" ou a usar informações de chunks irrelevantes que o retriever possa ter retornado.
    
3. **Ancoragem (Grounding):** Baseia suas alegações factuais _apenas_ no contexto fornecido, evitando alucinações.
    
4. **Relevância:** Responde diretamente à pergunta original do usuário.
    
5. **Citação:** Cita as fontes corretamente.
    

O desafio é que, ao contrário do Recall do retriever, estas métricas são **altamente subjetivas**.

---

### 2. A Solução: "LLM-as-a-Judge" para Métricas Subjetivas

Como a "qualidade" é difícil de medir com métricas automatizadas simples, a abordagem padrão é usar **outra LLM como "juiz"** para avaliar a resposta. Isso permite uma avaliação escalável de critérios subjetivos. A biblioteca _open-source_ **Ragas** é um exemplo popular que implementa isso.

---

### 3. Métricas Específicas (Ex: Biblioteca Ragas)

A Ragas fornece métricas que usam chamadas de LLM para pontuar a qualidade da geração.

#### Response Relevancy (Relevância da Resposta)

- **Pergunta que responde:** A resposta gerada está _no tópico_ da pergunta original?
    
- **Ponto-chave:** Esta métrica **ignora a precisão factual**. Ela apenas mede a relevância semântica entre a pergunta e a resposta.
    
- **Como Funciona (Processo Técnico):**
    
    1. O sistema pega a **resposta final** gerada pela LLM do RAG.
        
    2. Ele alimenta esta resposta em uma LLM "juiz" e pede: "Gere 5 perguntas que poderiam ter resultado nesta resposta."
        
    3. O sistema então vetoriza a **pergunta original** do usuário e as **5 perguntas geradas** pelo "juiz".
        
    4. Ele calcula a **similaridade de cosseno** média entre o vetor da pergunta original e os vetores das perguntas geradas.
        
    5. Um score alto significa que a resposta estava alinhada com a intenção da pergunta.
        

#### Faithfulness (Fidelidade / Grounding)

- **Pergunta que responde:** A resposta está _ancorada_ (baseada) no contexto fornecido? (Esta é a métrica anti-alucinação).
    
- **Como Funciona (Processo Técnico):**
    
    1. Uma LLM "juiz" analisa a **resposta final** e extrai todas as **"alegações factuais"** (claims) feitas nela.
        
    2. Para _cada alegação_ extraída, o sistema faz uma nova chamada de LLM, perguntando: "Esta alegação é suportada pelo [contexto recuperado]?"
        
    3. O score final é a **porcentagem de alegações que foram suportadas** pelo contexto.
        

Outras métricas na Ragas usam abordagens similares (LLM-as-a-judge) para avaliar a sensibilidade ao ruído ou a qualidade da citação.

---

### 4. Avaliação em Larga Escala: Teste A/B e Feedback Humano

Uma alternativa ao LLM-as-a-judge é usar métricas de todo o sistema, focadas no usuário, através de **Testes A/B**.

- **Como Funciona:** O objetivo é medir o impacto de uma mudança _apenas_ no componente LLM (ex: ajustar o `System Prompt` ou mudar o `temperature`).
    
- **Processo:**
    
    1. **Grupo A:** 50% dos usuários recebem o `System Prompt` antigo.
        
    2. **Grupo B:** 50% dos usuários recebem o `System Prompt` novo.
        
    3. Ambos os grupos usam _exatamente_ o mesmo retriever.
        
    4. O engenheiro mede a métrica de satisfação do usuário (ex: a taxa de "polegar para cima" / "polegar para baixo").
        
- **Resultado:** Se a satisfação do Grupo B for estatisticamente maior, pode-se atribuir a melhoria diretamente à mudança no prompt da LLM.
    

### 5. Conclusão Estratégica

A avaliação da LLM em um RAG é inerentemente subjetiva. Requer o uso de avaliadores (seja um **LLM-as-a-judge** como o Ragas, para métricas granulares como _Faithfulness_, ou **feedback humano** para métricas holísticas como a satisfação) para tomar decisões informadas sobre ajustes de prompt e seleção de modelo.