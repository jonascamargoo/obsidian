
## O que é?

Chain-of-thought (CoT) prompting é uma técnica usada em modelos de linguagem, como o GPT, que visa melhorar a capacidade do modelo de raciocinar de maneira mais lógica e detalhada ao responder perguntas complexas. Em vez de solicitar uma resposta direta e imediata, o **CoT prompting** incentiva o modelo a pensar em voz alta, ou seja, a **quebrar o raciocínio em etapas sequenciais**.

A ideia por trás dessa técnica é que, ao "explicar" cada passo do raciocínio antes de chegar à conclusão final, o modelo tem uma chance maior de chegar a uma resposta correta ou bem fundamentada, especialmente em tarefas de raciocínio matemático, lógico ou analítico.

Por exemplo:

**Pergunta sem CoT prompting:**

- Qual é a soma de 35 + 47?

**Resposta direta:**

- 82.

**Pergunta com CoT prompting:**

- Pense passo a passo: qual é a soma de 35 + 47?

**Resposta com CoT prompting:**

- Primeiro, somamos as dezenas: 30 + 40 = 70.
- Depois, somamos as unidades: 5 + 7 = 12.
- Por fim, somamos os dois resultados: 70 + 12 = 82.

Ao usar o método **Chain-of-Thought**, o modelo explica seu processo de raciocínio, o que torna suas respostas mais precisas em questões que exigem uma abordagem estruturada.


## Exemplo de Prompt

Escreva um e-mail de vendas para meu curso Cria Atividade. Siga esses passos para escrever o melhor e-mail de vendas possível:

No título faça uma promessa curta que gera desejo para abrir, que seja uma solução para o principal problema desse público-alvo.

O público-alvo são empreendedores que criam conteúdo para o Instagram, com uma média de idade entre 24-35 anos. 

Escreva de maneira informal, amigável, mas polidamente. Comece com uma breve história para deixar uma leitura engajadora. Insira metáforas para explicar algo. 

Mapeie quais são os problemas que esses empreendedores enfrentam para criar e vender seus produtos no Instagram, que o Cria Atividade ajudará a resolver. 

Considere que palavras como "sucesso", "alavancar resultados" estão batidas, e esse público não gosta de ver essas palavras associadas a algo que vão comprar. 

Não escreva algo que se pareça com um tele-comercial, por exemplo: "Você sente dores nas costas? Aqui está a solução inovadora". 

Não escreva dessa maneira. Escreva na perspectiva de um empreendedor criativo que já passou pela jornada e tem o resultado que o público-alvo deseja passar. 

Cite os benefícios que o Cria Atividade tem sob seus concorrentes. 

Demonstre com sutileza como a vida desses empreendedores criativos serão impactadas e transformadas ao fazer o curso Cria Atividade.

Faça uma chamada para ação com um link para garantir a vaga no Cria Atividade.