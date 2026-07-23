---
tipo: conceito
area: IAs
tags:
- ia
criada: '2025-03-19'
---

## O que é?

Devemos lembrar que LLM é apenas um gerador de token. Então, como é possível que exista agentes virtuais? Operadores? Como eles executam funções no sistema operacional? 
## Como funciona?

O fluxo funciona da seguinte maneira: a aplicação de IA, como o ChatGPT, utiliza um modelo de linguagem (LLM), como o GPT-4o, para processar e gerar respostas. Além disso, a aplicação conta com diversas ferramentas auxiliares, como o gerenciamento de histórico de chat e outros mecanismos de suporte.

É importante destacar que essas ferramentas internas da aplicação não fazem parte do código gerado pela LLM. Muito provavelmente, são códigos altamente otimizados desenvolvidos por engenheiros humanos, garantindo eficiência e segurança no funcionamento da aplicação.

O **Managed Chat History** utiliza um **prompt global**, chamado **System Prompt**, que define um padrão para as respostas do modelo. Esse prompt global proporciona uma forma padronizada de retorno, contribuindo para a consistência e a coerência das interações ao longo da conversa.

![[Pasted image 20250319132933.png]]

Respondendo a pergunta do início, as LLMs não executam essas ações, elas apenas fornecem o retorno para o parâmetro de consulta definido fora da LLM.


```js
let history = [
  ...history,
  {
    role: 'system',
    content: `
      You are a helpful assistant with access to these tools which you can use 
      if you need them to provide a meaningful response to the user query:
      - Web search: Use by outputting <WEB SEARCH>: <SEARCH QUERY></SEARCH QUERY>
    `,
  },
  {
    role: 'user',
    content: "Who's the current president of the USA?",
  },
  {
    role: 'assistant',
    content: '<WEB SEARCH>: <SEARCH QUERY>Current president of the USA</SEARCH QUERY>',
  },
  {
    role: 'assistant',
    content: 'Web search results: Donald Trump is the current president of the USA.',
  },
  .
  .
  .
];

```

## Tools

Especificamente, por exemplo, ao interagir com os modelos de IA da OpenAI por meio de sua API/SDKs, você não descreverá ferramentas conforme descrito acima. Em vez disso, a OpenAI expõe um recurso chamado “funções” por meio de sua API.

```js
const tools = [
  {
    type: 'function',
    name: 'get_weather',
    description: 'Get current temperature for a given location.',
    parameters: {
      type: 'object',
      properties: {
        location: {
          type: 'string',
          description: 'City and country e.g. Bogotá, Colombia',
        },
      },
      required: ['location'],
      additionalProperties: false,
    },
  },
];

const response = await openai.responses.create({
  model: 'gpt-4o',
  input: [
    { role: 'user', content: 'What is the weather like in Paris today?' },
  ],
  tools,
});
```

### Function calling

Behind the scenes, as feramentas ("functions") serão injetadas no System Prompt de alguma forma, restando para a OpenAI lidar com as complexidades gerenciar as ferramentas.

```js
import { OpenAI } from "openai";

const openai = new OpenAI();

const tools = [{
    "type": "function",
    "function": {
        "name": "get_weather",
        "description": "Get current temperature for a given location.",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "City and country e.g. Bogotá, Colombia"
                }
            },
            "required": [
                "location"
            ],
            "additionalProperties": false
        },
        "strict": true
    }
}];

const completion = await openai.chat.completions.create({
    model: "gpt-4o",
    messages: [{ role: "user", content: "What is the weather like in Paris today?" }],
    tools,
    store: true,
});

console.log(completion.choices[0].message.tool_calls);


// Output
[{
    "id": "call_12345xyz",
    "type": "function",
    "function": {
        "name": "get_weather",
        "arguments": "{\"location\":\"Paris, France\"}"
    }
}]

```

![[Pasted image 20250319144905.png]]
https://platform.openai.com/docs/guides/function-calling?api-mode=chat&lang=python



## A grande questão

Considerando que as aplicações já possuem suas tools, o que eu poderia fazer para utilizar minhas próprias tools customizadas? Há duas formas. A primeira consiste em provar que minha aplicação é tão especial que os provedores de IA deveriam incluir ferramentas específicas em sua base de código para atender minhas necessidades. A segunda forma é a mais fácil, utilizando o [[MCP|Protocolo de Contexto de Modelo (MCP)]].


