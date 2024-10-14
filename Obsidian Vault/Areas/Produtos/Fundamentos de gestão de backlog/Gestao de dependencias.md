
## O que é?

Dependências são relações entre diferentes itens de trabalho que impactam a sequência ou a possibilidade de conclusão de uma tarefa. Elas determinam a ordem em que as atividades devem ser realizadas, sendo cruciais para garantir que o fluxo de trabalho aconteça sem impedimentos ou bloqueios. As dependências podem existir dentro de um time ou entre diferentes equipes, impactando diretamente o cronograma e a capacidade de entrega.

Dependências mal gerenciadas podem gerar atrasos, retrabalho e desalinhamento, por isso é fundamental que sejam identificadas e monitoradas continuamente.


![[Pasted image 20240927153659.png]]



## Tipos de Dependências

### 1. **Dependência Interna**

- **O que é**: Essas dependências estão totalmente sob o controle do time. São itens de trabalho que precisam ser concluídos em sequência dentro do próprio fluxo da equipe.
- **Exemplo**: A equipe de desenvolvimento de software não pode testar uma funcionalidade até que o código tenha sido concluído.

### 2. **Dependência Externa**

- **O que é**: Dependências fora do controle do time, onde há interação com entregas de outras equipes ou fornecedores. Esse tipo de dependência costuma trazer mais risco, já que os times não controlam diretamente o andamento da atividade.
- **Exemplo**: A equipe de produto depende de uma API desenvolvida por outro time para integrar uma nova funcionalidade ao produto.

### 3. **Dependência Obrigatória**

- **O que é**: São dependências críticas, ou seja, não é possível avançar para o próximo estágio ou completar uma tarefa sem resolver essa dependência. Elas devem ser providenciadas para evitar bloqueios.
- **Exemplo**: Para lançar um aplicativo no mercado, é obrigatório que ele seja aprovado pelas lojas de aplicativos, como a App Store ou Google Play.

### 4. **Dependência Opcional**

- **O que é**: Dependências que podem ou não ser resolvidas, dependendo da priorização do time. A falta de resolução não necessariamente impede o andamento do projeto, mas pode melhorar a qualidade ou eficiência.
- **Exemplo**: A equipe pode decidir integrar uma ferramenta de analytics no produto agora ou postergá-la para uma versão futura, sem impactar a funcionalidade principal do lançamento.

## Lista de Dependências

A lista de dependências é um registro que documenta todas as dependências identificadas em um projeto, categorizando-as como internas, externas, obrigatórias ou opcionais. O objetivo é garantir que a equipe tenha visibilidade total sobre os fatores que podem impactar a entrega e que possam planejar e mitigar riscos de forma proativa.

### Como documentar?

1. **Nome da Dependência**: Um título breve para identificar a dependência.
2. **Tipo**: Identifique se é interna, externa, obrigatória ou opcional.
3. **Descrição**: Detalhe o que é necessário para resolver a dependência.
4. **Responsável**: Quem está responsável por resolver ou monitorar a dependência.
5. **Data estimada**: Previsão de quando a dependência será resolvida.
6. **Riscos**: Quais os possíveis impactos no projeto se a dependência não for resolvida.
7. **Status**: Atualize com o progresso (pendente, em andamento, resolvida).

### Exemplo de Lista de Dependências:

|Nome da Dependência|Tipo|Descrição|Responsável|Data Estimada|Riscos/Impactos|Status|
|---|---|---|---|---|---|---|
|API de autenticação|Externa, Obrigatória|Dependência de API desenvolvida por outro time|Time de Backend|2 semanas|Atraso no lançamento|Pendente|
|Testes de QA|Interna, Obrigatória|Testes unitários antes de deploy|Equipe de Qualidade|1 semana|Erros em produção|Em andamento|
|Documentação do Produto|Interna, Opcional|Atualizar a documentação para o usuário final|Time de Produto|3 semanas|Menor clareza para o cliente|Pendente|

## Recomendações gerais

1. Dê visibilidade de todas as dependências;
2. Monitore o prazo das dependências;
3. Utilize a lista de dependências no dia a dia, para saber se na data x, o dev que está pensando em puxar irá de fato conseguir. Não deixe a dependência virar um impedimento.
