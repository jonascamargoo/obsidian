A geração de texto em LLMs não é um processo determinístico; é uma **escolha aleatória ponderada** executada token por token. Em cada etapa, a LLM gera uma distribuição de probabilidade sobre todo o seu vocabulário (ex: 100.000 tokens) para prever o próximo token.

A forma dessa distribuição de probabilidade indica a "certeza" do modelo:

- **Distribuição "Spiky" (Pontuda):** Alta confiança. Um ou poucos tokens (ex: "azul") têm uma probabilidade muito alta, e todo o resto é próximo de zero.
    
- **Distribuição "Flat" (Plana):** Incerteza. Muitos tokens têm probabilidades baixas, mas semelhantes, sem um vencedor claro.
    

"Tunar" (ajustar) o comportamento da LLM é, na verdade, o processo de manipular essa curva de distribuição antes que a escolha aleatória (amostragem) seja feita.

---

### 1. A Abordagem Determinística: Greedy Decoding

A forma mais simples de amostragem é eliminar a aleatoriedade.

- **Como Funciona:** Ignora a probabilidade e **sempre escolhe o token com a maior pontuação** (`max(probability)`).
    ![[Pasted image 20251103185219.png]]
- **Prós:**
    
    - **Determinístico:** A mesma entrada (prompt) sempre gerará a mesma saída.
        
    - Útil para debugging, testes e tarefas que exigem consistência (ex: geração de código).
        
- **Contras:**
    
    - Produz texto previsível, genérico e "sem graça".
        
    - **Risco de Loops:** O modelo pode facilmente ficar preso em loops de repetição (ex: "eu sou eu sou eu sou..."), pois se "sou" for o token mais provável após "eu", ele sempre o escolherá.
        

---

### 2. Parâmetros de Manipulação da Distribuição

Como o Greedy Decoding é muito limitado, a maioria das aplicações usa amostragem aleatória, controlada pelos seguintes parâmetros.

#### 🌡️ Temperature (O "Botão" da Criatividade)

Este é o parâmetro mais comum. A temperatura **redefine a forma** da distribuição de probabilidade _antes_ da amostragem.
	![[Pasted image 20251103185506.png]]
- `Temperature = 1`: Usa a distribuição original, sem alterações.
    
- `Temperature < 1` (ex: 0.8): "Esfria" a distribuição, tornando-a **mais "spiky"**. As probabilidades altas ficam ainda mais altas, e as baixas, mais baixas. O resultado é mais conservador e focado.
    
- `Temperature = 0`: É o caso especial que **se torna o Greedy Decoding**. A probabilidade do token de topo vai para 100%.
    
- `Temperature > 1` (ex: 1.3): "Aquece" a distribuição, tornando-a **mais "flat"**. Isso aumenta a probabilidade de tokens mais raros serem escolhidos, levando a resultados mais "criativos", variados ou, se muito alto, incoerentes.
    

#### ✂️ Top-K Sampling (Truncamento Estático)

Isso define um limite rígido sobre _quantos_ tokens podem ser escolhidos.

- **Como Funciona:** O modelo **filtra** a distribuição para incluir apenas os `K` tokens de maior probabilidade. A amostragem aleatória (ponderada pela temperatura) é então realizada _apenas_ nesse subconjunto.
    ![[Pasted image 20251103185804.png]]
- **Exemplo:** `top_k = 5`. O modelo só pode escolher entre os 5 tokens mais prováveis, ignorando todo o resto.
    
- **Problema:** É estático. Se o modelo está muito confiante (P="azul" 99%), `top_k=5` ainda permite a chance de escolher 4 outras opções. Se está incerto (distribuição plana), `top_k=5` pode cortar opções viáveis.
    

#### 🎯 Top-P (Nucleus) Sampling (Truncamento Dinâmico)

Esta é uma abordagem mais inteligente e responsiva, geralmente preferida ao Top-K.

- **Como Funciona:** Em vez de um número fixo de tokens (`K`), você define um **limite de probabilidade cumulativa** (`P`). O modelo seleciona o conjunto mínimo de tokens (o "núcleo") cuja probabilidade somada seja maior que `P`.
    ![[Pasted image 20251103185722.png]]
- **Exemplo:** `top_p = 0.85` (85%).
    
    - **Cenário 1 (Confiante):** Se `P(azul)=0.90`. O "núcleo" conterá apenas 1 token ("azul"), pois ele sozinho já excede 0.85.
        
    - **Cenário 2 (Incerto):** Se `P(token1)=0.3`, `P(token2)=0.2`, `P(token3)=0.1`, `P(token4)=0.1`, `P(token5)=0.1`, `P(token6)=0.05`... O "núcleo" incluirá os tokens de 1 a 5 (pois 0.3+0.2+0.1+0.1+0.1 = 0.8) e talvez o 6, até que a soma atinja 0.85.
        
- **Benefício:** É dinâmico. Permite que o modelo seja conservador quando está confiante e criativo quando está incerto.
    

---

### 3. Ajustes Adicionais (Bias e Penalidades)

#### 🔄 Repetition Penalty (Penalidade de Repetição)

Usado para combater os loops de repetição.

- **Como Funciona:** Um multiplicador (ex: `1.2`) que **reduz a probabilidade** de tokens que já apareceram recentemente na conclusão. Um valor maior que 1 penaliza, e um valor menor que 1 recompensa (não usual).
    ![[Pasted image 20251103190144.png]]

#### 🚫 Logit Bias (Viés de Logit)

Permite o controle manual e permanente de tokens específicos.

- **Como Funciona:** Você passa um mapa que **aumenta ou diminui** a probabilidade de tokens específicos (pelo seu ID) _antes_ de qualquer amostragem.
    ![[Pasted image 20251103190154.png]]
- **Casos de Uso:**
    
    - **Negativo:** Diminuir drasticamente a probabilidade de palavrões ou tokens indesejados.
        
    - **Positivo:** Em uma tarefa de classificação RAG, você pode aumentar a probabilidade dos tokens de categoria (ex: "Fato", "Opinião") para forçar o modelo a escolher entre eles.
        

---

### 🏁 Estratégia Prática

Ajustar esses parâmetros é um ato de equilíbrio:

1. **Para Fatos, Código ou RAG (Foco na Precisão):** Use uma **temperatura baixa** (ex: `0.2` a `0.8`) e **Top-P** (ex: `0.9`). Isso mantém a resposta "ancorada" no contexto e nos fatos, mas permite alguma fluidez na linguagem.
    
2. **Para Geração Criativa (Marketing, Poesia):** Use uma **temperatura mais alta** (ex: `1.0` a `1.2`) e um **Top-P** (ex: `0.9` ou `1.0`).
    
3. **Para Problemas Específicos:** Se o modelo estiver se repetindo, adicione um `repetition_penalty`. Se estiver usando palavras erradas, use `logit_bias`.
    

Uma combinação de propósito geral sensata é: `temperature=0.8`, `top_p=0.9`, e `repetition_penalty=1.2`.