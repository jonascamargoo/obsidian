Um RAG de produção precisa lidar com um problema central: os usuários interagem de forma **conversacional**, o que gera prompts (consultas) péssimos para a recuperação de dados.

O prompt "Eu estava passeando com minha cachorra Poppy quando... meu ombro ficou dormente" é terrível para um banco de dados vetorial. O retriever precisa, portanto, **analisar e transformar** a consulta antes de enviá-la ao banco.

---

### 1. A Solução Padrão: Reescrita de Consulta via LLM (Query Rewriting)

Esta é a técnica mais simples e amplamente utilizada, justificando quase sempre o custo de uma chamada extra à LLM.

- **Como Funciona:** Uma LLM (ex: GPT-4o) atua como um "pré-processador" da consulta. Ela recebe um prompt de sistema detalhado para "limpar" a entrada do usuário.
    
- **Exemplo de Instrução (Prompt de Sistema):**
    
    > "Você é um especialista em reescrever consultas médicas. A consulta do usuário... reescreva-a para otimizar a busca em um banco de dados médico, fazendo o seguinte:
    > 
    > 1. Clarifique frases ambíguas.
    >     
    > 2. Use terminologia médica aplicável.
    >     
    > 3. Adicione sinônimos para aumentar a chance de _match_.
    >     
    > 4. Remova informações desnecessárias ou distrativas (ruído)."
    >     ![[Pasted image 20251102173442.png]]
    
- **Resultado:** A consulta conversacional sobre a "cachorra Poppy" é transformada em uma consulta otimizada para busca:
    
    > "Experienciou um puxão súbito e forte no ombro, resultando em dormência persistente no ombro e formigamento nos dedos por três dias. Quais são as causas potenciais ou diagnósticos, como neuropatia ou pinçamento de nervo?"
    > ![[Pasted image 20251102173539.png]]
    

---

### 2. Técnicas Avançadas de Análise

Embora a reescrita básica seja geralmente suficiente, técnicas mais complexas existem para extrair mais informações da consulta.

#### 2.1. Reconhecimento de Entidade Nomeada (NER)

- **Como Funciona:** Um modelo de NER (ex: Gliner) é usado para analisar a consulta e **rotular categorias** de informação (pessoas, datas, locais, livros, etc.).
    
- **Propósito:** Os rótulos extraídos não são usados para a busca vetorial em si, mas sim para alimentar de forma inteligente o **Metadata Filtering**.
    
- **Exemplo:** Se a consulta for "O que Harry Potter fez em 1993?", o NER extrai:
    
    - `person: "Harry Potter"`
        
    - `date: "1993"`
        
- O retriever pode então usar esses dados para filtrar os resultados onde `character == "Harry Potter"` E `year == "1993"`.
    ![[Pasted image 20251102173849.png]]

#### 2.2. Hypothetical Document Embeddings (HyDE)

Esta é uma técnica avançada que resolve um problema fundamental da busca semântica: a **disparidade de modalidade** (o "problema das maçãs e laranjas").

Normalmente, você compara um vetor de uma _pergunta_ (curta, interrogativa) com um vetor de uma _resposta_ (longa, declarativa). Seus vetores podem não ser tão próximos no espaço vetorial.

O HyDE resolve isso comparando "maçãs com maçãs" (resposta-com-resposta).

- **Como Funciona (O Fluxo):**
    
    1. O usuário envia a consulta (ex: "O que é HNSW?").
        
    2. Uma LLM é usada para **gerar um documento hipotético** que seria a _resposta perfeita_ para essa pergunta (ex: "HNSW, ou Hierarchical Navigable Small World, é um algoritmo de ANN...").
        
    3. Este **documento hipotético** (e não a consulta original) é então vetorizado (embedded).
        
    4. O vetor resultante deste documento falso é usado para realizar a busca ANN no banco de dados.
        
- **Resultado:** O sistema agora procura por documentos reais que sejam semanticamente similares a uma "resposta ideal", o que provou melhorar a performance da recuperação.
    

---

### 🏁 Estratégia e Conclusão

1. Ter alguma forma de análise de consulta é **fundamental** em um sistema RAG.
    
2. Na maioria dos casos, a **Reescrita de Consulta via LLM** é a abordagem correta, oferecendo o melhor equilíbrio entre custo, latência e melhoria de qualidade.
    
3. Técnicas avançadas como NER e HyDE podem oferecer benefícios adicionais, mas aumentam a complexidade e a latência. Elas devem ser **experimentadas e validadas com métricas** (Precision@K, MAP) para justificar sua implementação.