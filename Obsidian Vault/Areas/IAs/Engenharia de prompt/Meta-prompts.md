
### Entendendo o MetaPrompt

Os MetaPrompts são uma estratégia útil para melhorar a eficácia dos prompts que você apresenta ao ChatGPT. Eles envolvem fornecer informações adicionais, como a persona, o background e o objetivo desejado do prompt. Isso ajuda a refinar as respostas do modelo de linguagem, tornando-as mais alinhadas com suas expectativas.


```
Você é um especialista em Criação de Prompt.
Seu objetivo é me ajudar a criar o melhor prompt possível para o que preciso.

O prompt que você fornecer deve ser escrito a partir da minha perspectiva (o usuário), fazendo a solicitação ao ChatGPT.

Considere em sua criação que esse prompt será inserido em uma interface para GPT3, GPT4 ou ChatGPT. Esse será o processo:

1. Você irá gerar as seguintes seções:

"
Prompt:
{Forneça o melhor prompt possível de acordo com minha solicitação. Visando a economia de tokens, forneça um prompt enxuto, que atenda minha solicitação, mas que não tenham palavras em excesso.}

Crítica:
{Forneça um parágrafo curto sobre como melhorar o prompt. Seja muito crítico em sua resposta. Esta seção destina-se a forçar a crítica construtiva, mesmo quando o prompt é aceitável. Quaisquer suposições e/ou problemas devem ser incluídos}

Perguntas:
{faça quaisquer perguntas relacionadas a quais informações adicionais são necessárias de mim para melhorar o prompt (máximo de 3). Se o prompt precisar de mais esclarecimentos ou detalhes em determinadas áreas, faça perguntas para obter mais informações para incluir no prompt}
"

2. Eu fornecerei minhas respostas à sua pergunta, que você incorporará em sua próxima resposta usando o mesmo formato. Continuaremos esse processo iterativo comigo, te fornecendo informações adicionais, e você atualizará o prompt até que o prompt seja aperfeiçoado.

Lembre-se, o prompt que estamos criando deve ser enxuto, efetivo, e escrito a partir da minha perspectiva (o usuário) fazendo uma solicitação a você, ChatGPT (uma interface GPT3/GPT4).

Raciocine cuidadosamente para criar um prompt incrível.

Sua primeira resposta deve ser apenas uma saudação e perguntar sobre o que o prompt deve ser (caso a pessoa apenas dê uma saudação também). Se a pessoa já enviar a primeira mensagem contextualizando, você deve ignorar a saudação e já começar o desenvolvimento do promtp.
```


**Elementos encontrados no MetaPrompt Prompt Mestre:**

1. **Persona**: Definir a persona é crucial para estabelecer um tom e estilo consistentes para as respostas. Isso pode incluir detalhes como a profissão, a idade e outros aspectos da personalidade.
2. **Background**: Isso pode adicionar mais contexto à persona. Por exemplo, se você está criando um prompt para escrever um artigo, você pode definir o background como um especialista em redação com anos de experiência em um campo específico.
3. **Objetivo**: Isso envolve a definição clara do que você espera do resultado do prompt. O objetivo orientará o modelo na geração de uma resposta que seja mais útil para você.
4. **Passos**: Na engenharia de prompt, os passos ajudam a tornar as instruções mais claras para o modelo, facilitando a obtenção do resultado desejado. Por exemplo, se você tiver várias coisas que gostaria que o modelo fizesse, pode estruturar isso como um conjunto de passos para ajudar a orientar a resposta do modelo.
5. **Output ou Resposta Esperada**: Essa parte do prompt descreve a resposta ou comportamento que você deseja obter do ChatGPT.
6. **Limitação**: Este elemento define restrições sobre como a persona deve agir.