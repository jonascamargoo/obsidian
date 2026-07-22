+Surgiu da metodologia ágil XP

## Os 3 C's de uma história de usuário são: 
Cartão, conversação e confirmação

### Cartão
Uma história de usuário é escrita em um cartão e este contém somente as informações necessários para nos lembrar do que a história se refere

### Conversação
Uma história de usuário é uma promessa de conversa futura. Os demais detalhes serão comunicados através de conversas.

![[Pasted image 20240923171859.png]]
### Confirmação
Os critérios de aceite fornecem informação suficiente para garantir que a história foi implementada corretamente.



## INVEST

É um acrônimo que descreve as 6 principais características de boas histórias de usuário.
### Recomendações

1. Após cada atividade de refinamento, verifique se as histórias de usuário atendem aos critérios INVEST.
2. Essas práticas variam de time para time!
### Independente
Se temos a história a, b ou c, elas podem ser desenvolvidas em qualquer ordem. Não podemos ficar limitados por motivo de "isso deve ser feito antes daquilo". 

Ex: Ainda na funcionalidade de Encontrar Pessoas, temos as histórias de Usuário: 1 - "como cliente, eu quero filtrar as pessoas para visualizar apenas as que me agradam"; 2 - "Como cliente eu quero consultar a foto da pessoa para verificar se eu simpatizo com ela". 3 - Como cliente, eu quero dar um match para mostrar que eu curti a pessoa. Essa é a ordem natural, mas não a única possível!

#### Dependência técnica
Para um usuário dar match com uma pessoa no app de relacionamento, ela, primeiramente, deve estar registrada! Falso, não necessariamente. O dev pode inserir uma pessoa no banco de dados manualmente, caso necessário. "*Não deixe* uma dependência técnica impedir a prioridade do negócio!"

#### Como remover a dependência técnica?

1. Aglutine histórias de usuário dependentes.
2. Reescreva as histórias de forma a remover a dependência

#### Recomendações

1. Não deixe que a ordem natural se transforme sempre na ordem final
2. Quando removemos a dependência técnica, damos mais poder ao negócio!
3. Puxar para implementação diferente da ordem natural não é tão óbvio assim, mas é sim possível.

## Negociável
Uma história negociável é aquela que  é um lembrete para uma conversa futura e não um contrato. *Negociável* está relacionada a quantidade de detalhes. Quanto mais detalhes, menor a possibilidade de discussão, pois muitas coisas já estariam definidas.

#### História de usuário x Requisito tradicional

A **história do usuário** e o **requisito tradicional** são formas diferentes de capturar o que um produto ou recurso precisa fazer, mas com enfoques distintos. A história do usuário tende a ser mais flexível, colaborativa e orientada a entregar valor ao usuário de forma iterativa, enquanto os requisitos tradicionais são mais formais e detalhados desde o início, o que pode engessar um pouco o processo.

- **História do usuário** = Foco no **"o que"** o usuário precisa e **por quê**.
- **Requisito tradicional** = Foco em **"como"** o sistema deve funcionar e suas especificações.

![[Pasted image 20240925130238.png]]

#### Recomendações
1. Não detalhe excessivamente a história de usuário ao criá-la no backlog pela primeira vez.
2. Foque no porquê e não apenas no como a história tem que ser desenvolvida.
3. Negociar uma história de usuário significa discutir sobre sua validade, ou seja, o porquê, com a parte interessada.
## Valorosa

Uma história valorosa é aquela que entrega algum tipo de benefício ou resultado para quem utiliza o produto de software. Benefício esse que está ligado a: redução, aumento, melhoria, acesso, etc.

Ex de história não valorosa: "Como cliente eu quero filtrar pessoas". Qual o benefício disso? Outro exemplo "Como cliente eu quero filtrar pessoas para que o negócio possa mostrar o maior número de pessoas e passe maior tempo dentro do app. Isso não está na perspectiva do usuário e sim pra quem cria o produto.

*O benefício ou resultado é para quem usa o produto*

Ex de uma história valorosa: "Como cliente, eu quero filtrar pessoas para visualizar apenas as pessoas que me agradam".

#### Recomendações
1. Ao escrever uma história, sempre se coloque no lugar de quem vai utilizar o produto.
2. Nunca adicione ao backlog uma história sem o valor declarado (cláusula *para*)
3. Em alguns casos, o beneficiário pela funcionalidade pode ser um usuário indireto.
## Estimável

Uma história estimável é aquela em que conseguimos fazer algum tipo de julgamento quanto ao esforço para entregá-la. Alguns tipos de estimativas: opinião do especialista, analogia, fórmulas, decomposição, etc. A técnica de tamanho de camisa serve como uma estimativa alto nível, sem muitos detalhes do funcionamento (tamanho P, M e G é uma aproximação). Após um tempo, já temos dados, insumos para fazer uma boa estimativa.

![[Pasted image 20240925134057.png]]

#### Estimativas são palpites...
Ao estimar, nos deparamos com vários elementos desconhecidos: domínio do negócio, tecnologia, relação com outra história, mudanças e externalidades.

#### Recomendações
1. Para estimar evite trabalhar com histórias grandes ou muito pequenas.
2. O processo de estimar não precisa ser algo pesado e massante.
3. Nem sempre precisamos de estimativa (o KANBAN mostra bem isso).
## Sob Medida

Uma boa história de usuário é escrita sob medida. Uma história sob medida é aquela que tem tamanho adequado ao contexto. *ESCALÁVEL*, peculiar e de time para time.

#### Tamanho da história no Scrum

Em Scrum é muito comum pensar se a história pode ser desenvolvida dentro de uma sprint, sem ter que transbordar para a próxima sprint? Se não, a história terá de ser fatiada.

![[Pasted image 20240925141759.png]]

E se o tempo da Sprint mudar? Isso deve ser levado em consideração ao criar as histórias.
#### Tamanho da história no Kanban

![[Pasted image 20240925145137.png]]


## Testável
Uma boa história testável é aquela que conseguimos verificar o seu comportamento e resultado. Uma **user story** que possui critérios de aceitação claros e objetivos, de forma que possa ser validada por testes. Ou seja, ela descreve não apenas a funcionalidade desejada, mas também **como saber se está funcionando corretamente**, permitindo que a equipe de QA ou automação consiga verificar se os requisitos foram atendidos.

Essencialmente, se não puder ser testada, a história não está "pronta" para desenvolvimento.

![[Pasted image 20240926112722.png]]

Ex de história testável: Na funcionalidade "Encontrar Pessoas", temos a seguinte história: "Como cliente, eu quero filtrar pessoas para visualizar apenas as pessoas que me agradam". [Critério de Aceite](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FProdutos%2FCriterios%20de%20Aceite): Permitir filtrar por cidade, estado e distância em KM.

### Recomendações
1. Criar bons critérios de aceite é fundamental para um bom desenvolvimento da funcionalidade.
2. Crie critérios de fácil entendimento.
3. Lembre-se que bons critérios contribuem para um desenvolvimento mais assertivo.