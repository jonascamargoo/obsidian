---
tipo: conceito
area: Produtos
tags:
- produto
criada: '2024-10-14'
---

## Definição

O backlog do produto é uma lista priorizada de itens que serão possivelmente desenvolvidos. "O backlog do produto é inerentemente incompleto".
## Algumas definições importantes

### Bug
 Um erro ou falha no código ou no funcionamento de um sistema que impede o comportamento esperado. Pode afetar a usabilidade, performance ou segurança. Ex: um botão não funcionando.

### Melhoria
 Alterações ou incrementos que tornam uma funcionalidade existente mais eficiente, fácil de usar, ou alinhada às necessidades dos usuários ou do negócio. Não é um defeito, mas uma otimização. Ex: melhorar o tempo de carregamento de uma página ou adicionar novos filtros de busca.

### Pesquisa
 Atividades de investigação para explorar uma nova ideia, hipótese ou solução. Normalmente envolve testes, estudos de viabilidade ou coleta de dados para orientar futuras decisões de produto. Ex:  pesquisar sobre o comportamento do usuário em relação a uma nova funcionalidade de personalização. Validação sempre!

### Dívida Técnica
 Decisões técnicas que priorizam soluções rápidas, mas não ideais, com o compromisso de serem corrigidas no futuro. Acumulada, pode comprometer a evolução do produto. Ex:  Um código mal estruturado, feito às pressas, que precisa ser revisado no futuro para evitar problemas de escalabilidade.
## Tarefa Técnica
 Trabalho relacionado à manutenção ou evolução da infraestrutura técnica, que pode não ter um impacto visível direto para o usuário, mas é essencial para a operação do produto. Melhoria não funcionais. Ex: Atualizar a versão de um framework usado no projeto ou melhorar a integração entre microserviços.
### Protótipo
 Uma versão inicial de um produto ou funcionalidade, construída rapidamente para testar conceitos, validação de hipóteses ou design. Normalmente não é funcional ou otimizado para produção. Ex: Um mockup interativo de uma nova interface de usuário para coletar feedback antes da implementação completa.

![[Pasted image 20240920145001.png]]

## Backlog DEEP

Um backlog sempre deve ser Detalhado, Estimado, Emergente e Priorizado

### Detalhado
Um backlog deve ser **claro** o suficiente para execução, mas **não detalhado demais** a ponto de gerar desperdício. Para alcançar esse equilíbrio, podemos usar a técnica do 20, 30, 50 onde:

- 20% das nossas histórias estão prontas para a sprint.
- 30% das nossas histórias são para as próximas 4 a 10 sprints.
- 50% das nossas histórias são para as próximas 10 ou mais sprints.


![[Pasted image 20240920142355.png]]
Para obter esse nível de detalhamento, o PO deve reservar cerca de 10% do tempo da sprint para reuniões de refinamento com o time. Uma boa prática é não fazer essas reuniões no começo ou final da sprint, pois costumam ser momentos de foco para o time.


### Estimado
Todos os itens têm uma [[Estimativa do backlog|**estimativa**]] pontual associada. Para isso, a história precisa estar descrita de forma clara, para que seja possível estimar e discutir sua complexidade.

### Emergente
O _backlog_ **evolui** para refletir o novo aprendizado, por isso, ele não pode ser imutável. Pelo contrário, o backlog pode e deve ser sempre atualizado, priorizado e reordenado para refletir o propósito e a visão do objetivo do produto ou projeto.

### Priorizado
[[Metodo ICE|Essa]] é a etapa **mais importante** para se obter **valor**. Por isso, evitaremos o conceito “tudo é prioridade”, pois como diz a máxima do dia a dia de projeto “quando tudo é prioridade, nada é prioridade”.

Voltando ao cenário citado anteriormente cujo projeto visa descartar um sistema legado, imagine que esse sistema faz emissão de notas fiscais e que ele esteja sofrendo degradação de performance na integração com o ERP devido ao alto volume de emissões. Saiba mais em [[Técnicas de Priorização]].




