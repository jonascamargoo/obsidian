## O que são?

Os critérios de aceite ou aceitação são uma lista de sentenças que definem aquilo que precisa ser verificado no item. São condições específicas e objetivas que uma **user story**  precisa atender para ser considerada completa. Eles funcionam como uma checklist de validação que garante que o que foi implementado está alinhado com as expectativas do usuário e do negócio. Se os critérios de aceite não forem cumpridos, a história não pode ser aprovada, ajudando a evitar ambiguidade no desenvolvimento e garantindo que o produto atenda aos requisitos definidos.

![[Pasted image 20240926123757.png]]

## Formatos

**Sentença Simples** é mais direta e serve para casos onde os critérios são claros e não dependem de variações complexas.
**Sentença Cenário** é útil quando você precisa considerar **contextos** e **comportamentos diferentes** para testar corretamente a funcionalidade.
#### Formato - Sentença Simples

**História de usuário:** "Como cliente, eu quero filtrar pessoas para visualizar apenas as pessoas que me agradam"
**Critério de aceite:**
	1. Permitir filtrar por cidade, estado e distância em KM;
	2. Mostrar resultados do filtro de 10 em 10 itens;
	3. Mostrar nome, cidade, estado e distância nos resultado do filtro.

Os critérios devem ser possíveis de responder com sim ou não, sem ambiguidade.

#### Formato - Sentença Cenário

**História de usuário:** "Como cliente, eu quero filtrar pessoas para visualizar apenas as pessoas que me agradam"
**Critérios de aceite**:
	1. Dado que o cliente não é pagante, quando o cliente filtrar por distância, então devem ser apresentados os resultado limitados a 10 pessoas.
	2. Dado que o cliente é pagante, quando o cliente filtrar por distância, então devem ser apresentados os resultados sem limitação e um percentual de compatibilidade de perfil da pessoa.

## Cenário - Modelo

Estrutura baseada em **BDD (Behavior Driven Development)**, e é utilizada para descrever o comportamento esperado de uma funcionalidade em um cenário específico.

#### Dado que (Given)

Dado que xxxxxxxxxxxx e xxxxxxxxxxxxx (condições necessárias para que o cenário aconteça);
- **Objetivo**: Define o **contexto** ou as **condições prévias** necessárias para que o cenário aconteça. Pode ser algo relacionado ao estado do sistema, as permissões do usuário ou informações já existentes.
- **Exemplo**: "Dado que o cliente não é pagante" ou "Dado que o usuário já fez login".
- **Uso**: Isso ajuda a criar o cenário no qual a funcionalidade será testada. Em um cenário de e-commerce, por exemplo, poderia ser "Dado que o carrinho contém 2 itens".

#### Quando (When)

Quando xxxxxxxxxxxxxx e xxxxxxxxxxxxx (eventos ou ações realizadas pelo usuário com a solução);
- **Objetivo**: Define a **ação** ou **evento** que desencadeia o comportamento que estamos testando. Isso pode ser uma interação do usuário com a interface, como clicar em um botão, ou uma mudança de estado no sistema.
- **Exemplo**: "Quando o cliente filtrar por cidade" ou "Quando o usuário clicar no botão de compra".
- **Uso**: Especifica a ação que resulta na execução da funcionalidade ou regra de negócio que será validada.

#### Então (Then)

Então xxxxxxxxxx e xxxxxxxxxxxxxx (respostas e/ou resultados da solução).
- **Objetivo**: Define o **resultado esperado** depois que a ação do "Quando" ocorrer. Deve ser algo observável e verificável, permitindo validar se a funcionalidade está correta.
- **Exemplo**: "Então deve mostrar os resultados limitados a 10 pessoas" ou "Então o pagamento deve ser confirmado".
- **Uso**: Descreve o efeito ou resposta do sistema que precisamos garantir após a ação. Isso pode ser, por exemplo, "Então o sistema deve exibir uma mensagem de sucesso".

## DoR vs DoD

### Definition of Ready (DoR) - Acordo

É um acordo entre Product Owner e devs sobre como os itens devem ser preparados para o desenvolvimento. É referente à qualidade do trabalho do PO!

Ex de Dor:
	1. Toda história tem de ter informado os três elementos: quem, o quê e para;
	2. Toda história tem que seguir os critérios INVEST;
	3. Todo bug tem que ter registrado os passos para reprodução do mesmo.

### Definition of Done (DoD)

É um acordo entre as pessoas do time sobre o que deve ser feito para se declarar um item como concluído. É referente à qualidade do trabalho do Dev!

Ex de Dod:
	1. Toda funcionalidade tem que ser submetida a testes;
	2. Toda funcionalidade deve atender a todos os critérios de aceite;
	3. O código tem que ter sido comitado na branch XPTO.
## O que guia o dev?

História e critérios de aceite!

Ele se pergunta: "a funcionalidade desenvolvida atende a DoD? Não? Volta pra desenvolvimento!"

## Recomendações gerais para os critérios de aceite

1. Não economize palavras para escrever os critérios;
2. Verifique os critérios antes, durante e depois do desenvolvimento;
3. Bons critérios de aceite ajudam ao desenvolvimento de uma funcionalidade que atende às necessidades do usuário.