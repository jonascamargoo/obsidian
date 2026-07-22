---
tipo: conceito
area: IAs
tags:
- ia/rag
criada: '2025-08-27'
---

A etapa final do RAG é injetar o contexto recuperado em um prompt e enviá-lo a uma LLM. Mas _por que_ isso funciona? Como a LLM consegue "dar sentido" a essa informação? A resposta está na arquitetura **Transformer**, especificamente no componente **Decoder**.

O artigo original de 2017, "Attention is All You Need", propôs uma arquitetura Encoder-Decoder (para tradução).

- **Encoder:** Especializado em "entender" e criar representações semânticas ricas (usado em modelos de embedding, como os Bi-Encoders).
    
- **Decoder:** Especializado em "gerar" texto com base em um entendimento contextual (o núcleo da maioria das LLMs modernas, como GPT).
---
### 1. A Jornada do Prompt (Processamento)

Quando uma LLM (Decoder-only) recebe seu prompt aumentado (consulta + contexto), ela passa por um processo de refinamento iterativo em várias camadas para _entender_ o texto antes de _gerar_ qualquer coisa.

####  Tokenização: O texto é quebrado em tokens.
    
#### Embeddings Iniciais (1º Palpite): Cada token recebe dois vetores:
    
Vetor de Embedding: Um "palpite inicial" estático sobre o significado do token (ex: o token "banco" sempre recebe o mesmo vetor inicial). Pensamos nele como a descrição de uma palavra no dicionário, com significado em sem semântica.

Vetor Posicional: Um vetor que informa a _localização_ do token no prompt (ex: 1º, 2º, 10º).
![[Pasted image 20251103111840.png]]

#### O Mecanismo de Atenção (O Mapeador de Relações):
Este é o coração do Transformer. Cada token "olha" para _todos os outros tokens_ no prompt (vendo seu "palpite de significado" e sua "posição"). Ele então decide quais tokens são mais importantes para definir o seu _próprio_ significado contextual. (Ex: o token "banco" vai prestar muita atenção em "dinheiro" ou "sentar", dependendo do contexto).
![[Pasted image 20251103113558.png]]

O trabalho do Mecanismo de Atenção é usar essa informação para gerar um **"Segundo Palpite"**: uma nova representação (vetor) para esse token, que agora está "consciente" do contexto ao seu redor.
##### Passo 1: Calcular os Scores (Afinidade)

O token "banco" pega no seu próprio vetor **Query (Q)** e "entrevista" todos os outros tokens (incluindo ele mesmo) usando os seus vetores **Key (K)**. Ele calcula um "score de afinidade" (geralmente através de um produto escalar - _dot product_) entre a sua Query e a Key de todos os outros.

```
Score_banco_sentei = Query_banco • Key_sentei
Score_banco_no      = Query_banco • Key_no
Score_banco_da      = Query_banco • Key_da
Score_banco_praça   = Query_banco • Key_praça
...
```

**Resultado:** Se o `Query_banco` estiver a "procurar" um contexto de localização (devido ao seu vetor posicional e ao significado de "banco"), ele terá uma afinidade (um _score alto_) com os vetores `Key` de "sentei" e "praça". Ele terá um _score baixo_ com `Key` de "dinheiro" (se essa palavra estivesse na frase).

##### Passo 2: Normalizar os Scores (Softmax)

Os scores brutos (ex: `15.2, 1.1, 1.5, 14.8`) não são úteis. Eles são passados por uma função **Softmax**, que os transforma numa distribuição de probabilidade (pesos) que soma 1.0.

- **Resultado (Pesos de Atenção):**
    
    - `sentei`: 0.45 (45% de atenção)
        
    - `no`: 0.05 (5% de atenção)
        
    - `da`: 0.05 (5% de atenção)
        
    - `praça`: 0.45 (45% de atenção)
        

Agora, o token "banco" "sabe" que, para entender o seu próprio significado neste contexto, ele deve prestar 45% de atenção a "sentei" e 45% a "praça".

##### Passo 3: Criar o "Segundo Palpite" (Média Ponderada)

O token "banco" usa estes pesos de atenção para criar o seu novo vetor (o "segundo palpite"). Ele faz isso calculando uma **média ponderada** dos vetores **Value (V)** de todos os outros tokens.

```
Segundo_Palpite_banco = (0.45 * Value_sentei) + 
                        (0.05 * Value_no) + 
                        (0.05 * Value_da) + 
                        (0.45 * Value_praça) +
                        ...
```

**Este é o resultado final:** O novo vetor para "banco" (o seu "segundo palpite") é, literalmente, uma mistura de 45% do significado de "sentei", 45% do significado de "praça", etc.

Ele deixou de ser o vetor ambíguo de "banco" (dinheiro OU assento) e tornou-se um vetor altamente contextualizado que significa "assento de praça".

#### Multi-Head Attention (Atenção Múltipla)
O Mecanismo de Atenção (com Q, K, V) que descrevemos é ótimo, mas tem uma limitação: ele só tem _um_ ponto de vista. Ao calcular a afinidade, ele pode aprender a focar em um tipo de relação (ex: relações gramaticais), mas pode acabar ignorando outras (ex: relações de sinônimos).

**A Solução:** Em vez de ter um único mecanismo de atenção, o Transformer executa vários deles **em paralelo**. Isso é a "Atenção Múltipla".

- **Analogia: Um Comitê de Especialistas** Pense no "Multi-Head" como um comitê de especialistas (ex: 12 cabeças/heads) olhando para a mesma frase. Cada especialista (cabeça) tem sua própria especialidade, porque eles foram treinados de forma independente.
    
    - **Head 1 (O Gramático):** Aprende a focar nas relações sujeito-verbo.
    - **Head 2 (O Temático):** Aprende a focar em palavras semanticamente similares (ex: "banco" e "praça").
    - **Head 3 (O Posicional):** Aprende a focar em palavras que estão "próximas" umas das outras.
        
- **O Processo:**
    
    1. Cada "cabeça" (head) realiza seu próprio cálculo de Atenção (Q, K, V) em paralelo, sem saber o que as outras estão fazendo.
    2. No final, para o token "banco", você não tem _um_ "segundo palpite", mas sim **12 "segundos palpites" diferentes** (um da perspectiva de cada "cabeça").
    3. O modelo então **concatena** (junta lado a lado) todos esses 12 vetores de resultado.
    4. Ele passa esse vetor gigante por uma camada final (uma pequena rede neural) para "misturá-los" e criar **um único vetor de saída unificado**.

- **Resultado:** O "segundo palpite" final é um vetor de significado extremamente rico, pois é o resultado de um "consenso" que considera 12 tipos diferentes de relações contextuais ao mesmo tempo. É isso que cria o "mapa de relacionamento extremamente detalhado".
![[Pasted image 20251103113902.png]]

####  Rede Feedforward (FFN) (O "Cérebro" do Conhecimento)

Até agora, o token "banco" foi enriquecido _apenas_ com informações de outros tokens na _mesma_ frase (ex: "sentei", "praça"). Ele ainda não "pensou" sobre o que essa nova informação significa no contexto do "conhecimento de mundo" geral.

É aqui que entra a Rede Feedforward (FFN).

- **O que ela faz:** A FFN é uma rede neural que processa o "segundo palpite" (o vetor que saiu da Multi-Head Attention) e o "enriquece" com o conhecimento de mundo aprendido durante o treinamento.
    
- **Analogia: O Processador Central** Se a Multi-Head Attention foi a "coleta de informações" (o token perguntou aos seus vizinhos o que eles achavam), a FFN é o **"processamento"**. O token pega todas essas opiniões e "pensa" sobre elas.
    
- **O Processo:**
    1. O vetor de saída da Multi-Head Attention (o "segundo palpite") é enviado para a FFN.
    2. **Importante:** Cada token passa por esta FFN de forma **independente** (mas a FFN é a _mesma_ para todos os tokens).
    3. A FFN é, de longe, a maior parte do modelo, é onde está a maioria dos parâmetros/neurônios. É o "músculo" computacional que armazena o "conhecimento" sobre fatos, linguagem, raciocínio, etc.
    4. Ela "pensa" sobre o vetor de entrada (ex: "Ah, este vetor representa um 'assento de praça'") e o transforma, aplicando seu conhecimento (ex: "Assentos de praça geralmente são de madeira ou concreto e usados para descanso").
    
- **Resultado:** A FFN gera um **vetor de saída final** para o token "banco" (vamos chamá-lo de "segundo palpite finalizado"). Este vetor agora não está apenas ciente de seu contexto _imediato_ ("sentei", "praça"), mas também está enriquecido pelo _conhecimento de mundo_ massivo do modelo.
---
####  Refinamento Iterativo (Camadas)

O processo (Multi-Head Attention -> FFN) constitui **uma única Camada (Layer) do Transformer**. O resultado é um vetor de token muito mais "inteligente" do que o "primeiro palpite".

A pergunta é: isso é suficiente?

A resposta do Transformer é "não". Para entender relações complexas, sarcasmo, causalidade de longo prazo, etc., o modelo precisa "pensar" sobre o seu próprio "pensamento".

- **O que é:** As LLMs não têm apenas _uma_ camada. Elas **empilham** essas camadas (de 8 a 64+).
    
- **O Processo (O Loop):**
    
    1. O "primeiro palpite" (Input) entra na **Camada 1**.
        
    2. A Camada 1 (com sua própria MHA e FFN) gera um "segundo palpite" (Output 1).
        
    3. Este "segundo palpite" (Output 1) torna-se o **Input** para a **Camada 2**.
        
    4. A Camada 2 (com sua _própria_ MHA e FFN) recebe o "segundo palpite" e o refina, gerando um "terceiro palpite" (Output 2).
        
    5. ...isso se repete por 8, 12, 64... camadas.
        
- **Analogia: O Processo de Pensamento Profundo**
    
    - **Camada 1 (Entendimento Superficial):** "Ok, o 'banco' aqui significa 'assento de praça'."
        
    - **Camada 2 (Entendimento Contextual):** "Entendido. A frase 'Sentei no banco da praça' descreve uma ação de descanso."
        
    - **Camada 10 (Entendimento Temático):** "Considerando o parágrafo anterior (sobre um dia estressante), esta frase sobre sentar na praça agora tem uma conotação de 'busca por paz' ou 'alívio'."
        
    - **Camada 30 (Entendimento Abstrato):** O modelo agora tem uma representação vetorial tão refinada que entende o tom, o sentimento e o propósito do texto.
        
- **Resultado:** A cada camada, o vetor de cada token se torna exponencialmente mais inteligente e ciente de relações cada vez mais distantes e abstratas. O vetor final, que sai da _última_ camada, é a representação de significado mais profunda que o modelo pode criar, e é esse vetor que é usado para gerar o próximo token.
![[Pasted image 20251103115414.png]]
---

### 2. O Loop de Geração (Token por Token)

Depois que o prompt passou por _todas as camadas_ (ex: 64) e os vetores de token estão altamente refinados, a geração começa.

1. **Distribuição de Probabilidade:** Com base nesses vetores finais, o modelo pergunta: "Com base no meu treinamento, qual token é o mais provável de vir a seguir?".
    
2. Ele calcula uma **probabilidade para _cada_ token em seu vocabulário** (ex: 100.000 tokens).
    
3. **Amostragem (Sampling):** O modelo **escolhe (sorteia) um token** dessa distribuição. Tokens com maior probabilidade são escolhidos mais frequentemente.
    
4. **Apêndice e Repetição:** O token escolhido é **anexado ao final do prompt**.
    
5. **O PROCESSO INTEIRO RECOMEÇA:** Para gerar o _segundo_ token de resposta, o modelo pega o (prompt original + primeiro token gerado) e o passa por _todas as 64 camadas_ novamente, gerando uma nova distribuição de probabilidade para o token seguinte.
    

Isso é repetido até que um limite de tokens seja atingido ou o modelo gere um token especial `[END_OF_COMPLETION]`.

---

### 3. Implicações para o RAG

Entender essa arquitetura explica _por que_ o RAG funciona e quais são suas limitações:
#### Por que o RAG Funciona
O RAG funciona porque o **Mecanismo de Atenção** é explicitamente projetado para analisar o contexto injetado (seus chunks recuperados) e entender sua relação com a consulta. A **Rede Feedforward** (FFN) então usa seu conhecimento de mundo para interpretar esse contexto e formular uma resposta.
#### Custo Computacional
#####  "A geração de _um único token_ é extremamente cara."

Quando pedimos a uma LLM para gerar uma resposta, ela não a escreve de uma vez. Ela gera a resposta **token por token** (palavra por palavra).

O ponto crucial é: para gerar o **Token nº 50**, o modelo não pode simplesmente olhar para o Token nº 49. Ele precisa **reler e reprocessar todo o histórico** (o prompt original + os 49 tokens que ele já gerou) _do zero_.

Isso acontece porque todo o histórico (ex: 50 tokens) é enviado para a Camada 1. A Camada 1 (Atenção + FFN) processa tudo e envia para a Camada 2, se repetindo até a última camada. Só então, após todo esse processamento massivo, o modelo calcula a probabilidade para gerar o **Token nº 51**.
##### "O custo cresce... (com) complexidade que se aproxima de $O(N^2)$."

Esta é a _razão_ pela qual o passo anterior é tão caro. $N$ aqui é o **comprimento da sequência** (o número de tokens no prompt + contexto).

O custo vem do **Mecanismo de Atenção**.  Imagine que cada token na sua sequência de entrada é uma "pessoa" em uma sala de reunião. Para que _uma_ pessoa (um token) saiba o que dizer (seu significado contextualizado), ela precisa "apertar a mão" e "conversar" com _todas as outras pessoas_ (tokens) na sala. Se você tem  pessoas na sala, __ pessoa precisa fazer  "conversas". Como _todas as $N$ pessoas_ precisam fazer isso ao mesmo tempo (para descobrir seu próprio contexto), o número total de "conversas" (interações) é $N \times N$, ou $N^2$.


Agora, vamos juntar tudo:

- **Cenário 1: LLM Simples**
    - **Prompt:** "Qual a capital do Canadá?"
    - **Comprimento (N):** $\approx$ 10 tokens.
    - **Custo de Geração (por token):** $\approx O(10^2) = O(100)$ interações por camada.
    
- **Cenário 2: RAG (com Contexto)**
    - **Prompt:** "Qual a capital do Canadá?"
    - - **Comprimento (N):** $\approx$ 10 tokens.
    - **+ Contexto:** (Adicionamos 4.000 tokens de chunks recuperados da Wikipedia sobre o Canadá).
    - **Comprimento atual (N):** $\approx$ 4.010 tokens.
    - **Custo de Geração (por token):** $\approx O(4010^2) = O(16.080.100)$ interações por camada.

O sistema RAG é mais caro não por causa da _busca_ (a busca vetorial é muito rápida), mas porque, por definição, ele **aumenta drasticamente o $N$ (comprimento da entrada)**.

Ao forçar a LLM a processar um prompt muito mais longo (consulta + contexto), o RAG empurra o custo da arquitetura Transformer para o seu limite quadrático. Cada token gerado pelo RAG custa ordens de magnitude a mais em computação do que um token gerado por uma consulta simples.

#### Aleatoriedade (Randomness):
A geração não é determinística; é **probabilística** (baseada em amostragem). Isso significa que, mesmo com o contexto perfeito injetado no prompt, a LLM pode **aleatoriamente escolher _não_ usar** essa informação e gerar uma resposta baseada apenas em seu conhecimento interno (FFN). Isso destaca a necessidade de técnicas de "grounding" (ancoragem) e prompts robustos.
