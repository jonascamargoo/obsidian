---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-11-04'
---

Alucinações (respostas plausíveis, mas factualmente incorretas) são uma preocupação constante em LLMs. Um sistema RAG é, em sua essência, a arquitetura mais eficaz para _reduzir_ alucinações, mas ele **não as elimina**.

Garantir que as respostas sejam "ancoradas" (grounded) no contexto recuperado é a parte mais importante da construção de um pipeline RAG confiável.

---

### 1. Por que o RAG Ainda Alucina? (A Causa Raiz)

LLMs não são bancos de dados que diferenciam "verdadeiro" de "falso". Elas são motores estatísticos que geram sequências de texto "prováveis" versus "improváveis". Uma alucinação é, por definição, uma **sequência de texto provável, mas factualmente incorreta**.

O RAG pode falhar de duas maneiras principais:

1. **Falha na Recuperação:** Se o retriever falhar em encontrar o documento correto, a LLM não terá escolha a não ser "inventar" uma resposta com base em seu conhecimento interno.
    
2. **Alucinação por Inferência (O Exemplo da Aula):** Este é o problema mais sutil.
    
    - **Consulta:** "Vocês oferecem desconto para estudantes?"
        
    - **Recuperador (Retriever):** Encontra Fato A ("desconto de 10% para idosos") e Fato B ("desconto de 10% para novos clientes").
        
    - **System Prompt:** "Seja prestativo."
        
    - **LLM (Alucinação):** A LLM "conecta os pontos" de forma incorreta. A sequência de texto mais _provável_ que é _prestativa_ e usa os _fatos_ recuperados é: "Sim, oferecemos 10% de desconto para estudantes, o mesmo ótimo desconto que oferecemos para idosos e novos clientes."
        
    - A LLM inventou um Fato C (desconto de estudante) porque parecia uma inferência provável a partir dos Fatos A e B.
        

---

### 2. Estratégias de Mitigação e Detecção

Como não há solução perfeita, uma abordagem de múltiplas camadas é necessária.

#### 2.1. Nível 1: Grounding via System Prompt (Mitigação)

Esta é a primeira e mais importante linha de defesa, onde você instrui o modelo sobre como ele deve se comportar.

- **Instrução de Ancoragem (Grounding):** O `System Prompt` deve ser explícito: "Responda à pergunta do usuário usando **apenas** os documentos fornecidos." ou "Se a resposta não estiver nos documentos, diga que você não sabe."
    
- **Instrução de Citação:** Forçar a LLM a citar suas fontes (ex: "Cite a fonte [doc:1] no final de cada frase.") _aumenta a probabilidade_ de ela realmente usar a fonte.
    
- **Falha (A Citação Alucinada):** A LLM pode simplesmente inventar uma citação (`[doc:2]`) para fazer a resposta _parecer_ ancorada, mesmo que a informação seja alucinada.
    

#### 2.2. Nível 2: Verificação Externa (Detecção Pós-Geração)

Como as citações podem ser alucinadas, a confiança real requer uma verificação externa (geralmente por outro modelo).

- **Self-Consistency (Auto-Consistência):** Uma abordagem sem base de conhecimento. Você executa o mesmo prompt várias vezes (com `temperature > 0`). Se as respostas factuais forem _inconsistentes_ entre as execuções, o modelo está provavelmente alucinando. (Desvantagem: caro e pouco confiável).
    
- **Verificadores de Citação (ex: ContextCite):** Esta é a solução robusta.
    
    1. A LLM gera a resposta e suas citações.
        
    2. O sistema (ex: ContextCite) recebe a resposta e os _chunks originais_ que foram enviados à LLM.
        
    3. Ele processa a resposta **sentença por sentença**.
        
    4. Para cada sentença, ele a compara com os documentos citados e atribui um rótulo (ex: `[fonte: doc_3]` ou, crucialmente, `[no source]`).
        
    5. Isso permite que o sistema filtre (ou sinalize) respostas que não podem ser verificadas contra o contexto fornecido.
        

#### 2.3. Nível 3: Benchmarking do Sistema (Avaliação Offline)

Isso não impede alucinações em produção, mas mede o quão bem seu sistema (RAG + Prompting + LLM) as evita, permitindo que você o ajuste.

- **Exemplo: ALCE Benchmark:** Este é um benchmark focado em RAG que mede três métricas-chave:
    
    1. **Fluency (Fluência):** O texto é bem escrito?
        
    2. **Correctness (Correção):** A resposta é factualmente precisa (comparada com o _ground truth_)?
        
    3. **Citation Quality (Qualidade da Citação):** As citações fornecidas estão corretas e alinhadas com as fontes?
        

---

### 3. Estratégia de Implementação (Resumo)

A luta contra as alucinações é um processo contínuo:

1. **Base:** Use RAG. É o passo mais eficaz para minimizar alucinações, fornecendo "ground truth" externo.
    
2. **Mitigação:** Refine seu `System Prompt` para forçar o _grounding_ e as _citações_.
    
3. **Validação:** Use benchmarks (como o ALCE) para avaliar o desempenho do seu sistema e ajustar seus prompts.
    
4. **(Opcional de Produção):** Para sistemas de alta confiabilidade (ex: médico, jurídico), implemente um verificador externo (como o ContextCite) para validar as respostas _antes_ de exibi-las ao usuário.