
![[Pasted image 20240920150011.png]]


## Épico

Um **épico** é uma grande iniciativa ou um conjunto de objetivos amplos que precisa ser dividido em funcionalidades menores para ser concluído. Ele geralmente abrange um escopo amplo de trabalho e pode envolver várias equipes ou sprints para ser totalmente realizado. Por exemplo, "Melhorar a experiência de pagamento" pode ser um épico, pois é um objetivo de alto nível que precisará ser dividido em partes menores. Ponto de vista -> Negócio. Tempo de desenvolvimento -> Meses. É o produto da estratégia de negócio para desenvolver um produto.

Ex: Implementar um novo sistema de pagamento internacional. Este épico inclui várias funcionalidades, como diferentes formas de pagamento, suporte para múltiplas moedas, integração com provedores de pagamento externos, etc. 

### Fatiando o produto por: papel (perfil ou Role-Based)

Quando você organiza épicos por **papel**, está focando nas necessidades e objetivos de **um tipo específico de usuário**. Neste caso, o épico descreve os principais objetivos e interações de um papel particular, e como aquele papel (persona) vai usar o sistema ou produto para atingir seus objetivos.

Utilizando um exemplo de app de relacionamento. Imaginamos duas personas: um que quer compromisso e outro que quer sexo. A partir daí, definimos dois épicos: "À procura de um novo amor" e "Apenas hoje e nada mais".

#### Características:

- Focado nas **necessidades e ações de um tipo de usuário específico**.
- Útil para **personalizar a experiência** e otimizar o sistema para diferentes papéis.
- Facilita o desenvolvimento de funcionalidades voltadas para **perfis de usuários** distintos (ex.: administrador, cliente, parceiro de negócios).

**Exemplo:**

- **Épico por papel:** "Funcionalidades para o administrador do e-commerce"
    - Funcionalidades dentro desse épico podem incluir:
        - Gerenciamento de inventário
        - Relatórios de vendas
        - Configuração de descontos e promoções
        - Aprovação de pedidos

Aqui, o foco está exclusivamente no **administrador** e nas tarefas que ele precisa realizar dentro do sistema, ignorando outros papéis como o cliente ou parceiro logístico.

#### Vantagens:

- Dá um entendimento claro das **responsabilidades e expectativas** de cada papel.
- Facilita a personalização e criação de **experiências distintas para diferentes perfis** de usuários.
- Útil quando o produto precisa atender a **diferentes perfis** de usuários com demandas bem diversas.

### Fatiando o produto por workflow

Utilizando um exemplo de produto "Aplicativo de Relacionamento".  Uma técnica muito utilizada é o  Storytelling. Vejamos:

` Você é uma pessoa solitária e conhece um aplicativo de relacionamento. Nesse aplicativo, você monta seu perfil com descrição e foto (perfil). Depois disso, vai em busca do amor, analisando o perfil das pessoas, da um like se gostar dela (relacionamento). Há uma área para ver quem deu match (administração) `

Com esse storytteling, os épicos foram definidos como perfil, relacionamento e administração.

Descrever épicos por **workflow** significa que você estrutura os épicos com base nas etapas ou fluxos de trabalho que os usuários (ou o sistema) seguem para realizar uma tarefa específica. Aqui, o foco é na **sequência de ações ou processos** pelos quais o usuário passa, independentemente do papel que ele desempenha.

#### Características:

- Baseado no **caminho** ou na **sequência de atividades** que o usuário realiza.
- Útil para **mapeamento de fluxos complexos** ou processos que envolvem várias etapas.
- Foco no **fluxo end-to-end** da funcionalidade, cobrindo todas as interações necessárias para atingir um objetivo.

**Exemplo:**

- **Épico por workflow:** "Processo de finalização de compra no e-commerce"
    - Funcionalidades dentro desse épico podem incluir:
        - Seleção de produtos
        - Cálculo de frete e imposto
        - Inserção de informações de pagamento
        - Confirmação do pedido

Aqui, o épico cobre todas as etapas que qualquer usuário pode seguir no processo de compra, sem focar em um papel específico.

#### Vantagens:

- Dá uma visão completa do processo.
- Ajuda a identificar gargalos ou pontos de fricção no **fluxo geral de trabalho**.
- Mais útil quando a preocupação é com **melhorias no processo** ou otimização da jornada do usuário.

### Quando usar cada abordagem?

- **Épicos por Workflow** são melhores quando você está melhorando **processos completos** que envolvem vários usuários ou sistemas (ex.: fluxo de checkout, onboarding, fluxo de suporte).
- **Épicos por Papel** são úteis quando diferentes tipos de usuários interagem de maneiras **muito distintas** com o produto (ex.: clientes, administradores, parceiros) e você quer otimizar essas experiências específicas.

## Funcionalidade

Uma **funcionalidade** (ou feature) é um componente ou uma parte do sistema que entrega um valor tangível e específico ao usuário. É aquilo que o produto faz ou pode fazer. Funcionalidades são partes menores e mais definidas de um épico, geralmente abordando uma necessidade específica dentro daquele escopo maior. Ponto de vista -> Produto. Tempo de dev -> Semanas

Ex:  **Funcionalidade dentro do épico de sistema de pagamento:** "Suporte para múltiplas moedas". Essa funcionalidade trata de uma parte específica do épico: a capacidade do sistema de aceitar diferentes moedas para transações.

### Para descrever as funcionalidades

1. Identifique aquilo que o usuário quer fazer e/ou os problemas que ele possui;
2. Identifique as funcionalidades que resolvem o problema.

Ex: Problema -> Me sinto sozinho e sem ninguém para conversar. Funcionalidades -> Encontrar pessoas e conversar com pessoas.

Recomendações:
1. Descreva as funcionalidades no modelo: infinitivo + complemento -> "encontrar algo"
2. Tenha sempre em mente os problemas que devem ser resolvidos
3. A funcionalidade está ligada ao valor de negócio (só implementada se de fato necessária)
## História de usuário

Uma **história de usuário** é uma descrição simples e concisa de uma funcionalidade, escrita da perspectiva do usuário. O objetivo é capturar o que o usuário precisa e o valor que ela traz. Normalmente segue o formato: "Como **tipo de usuário**, eu quero **funcionalidade** para **benefício esperado**." Ponto de vista -> Usuário. Tempo de desenvolvimento -> Dias.
### Modelo de história de usuário

Eu como... / quero... / para... -> Quem quer? / O que quer? / Por que quer?

Ex: Problema -> Me sinto sozinho e sem ninguém para conversar. Funcionalidades -> Encontrar pessoas e conversar com pessoas. Histórias de usuário -> Como cliente, quero filtrar pessoas para visualizar apenas as pessoas que me agradam; Como cliente, eu quero consultar a foto de perfil da pessoa para verificar se simpatizo com ela.

Para [saber mais](obsidian://open?vault=Obsidian%20Vault&file=Areas%2FProdutos%2FFundamentos%20de%20gest%C3%A3o%20de%20backlog%2FHist%C3%B3rias%20de%20usu%C3%A1rio).

### Recomendações 

1. As histórias de usuário devem ser escritas do ponto de vista de quem utiliza o produto;
2. As histórias de usuário devem ser escritas com foco no valor que será entregue para quem utiliza;
3. As histórias de usuário promovem a colaboração.

## Como esses conceitos se conectam?

- **Épico**: Grande objetivo que precisa ser desmembrado (ex.: novo sistema de pagamento).
- **Funcionalidades**: Partes específicas desse épico (ex.: múltiplas moedas, integração com gateways de pagamento).
- **Histórias de Usuário**: Explicam em detalhes o que cada funcionalidade precisa fazer do ponto de vista do usuário (ex.: permitir pagamentos em diferentes moedas).

### Exemplo do Produto Shopping

![[Pasted image 20240920152029.png]]

