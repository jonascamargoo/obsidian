

Preciso entender como o google drive sincroniza quandos usuários offline lidam com idempotencia.

Num sistema distruído com arquitetura centralizada, o servidor trabalha enviando réplicas dos dados para os clientes, nao o dado direto (apenas a réplica dele)). Quando minha conta da netflix, por exemplo, expira, como o servidor invalida o dado enviado via streaming (uma dica: é expirando as chaves primárias do documento). Fale sobre esses temas nesse contexto: Sincronicidade, regabilidade, dentre outros.  Caso de jogo demo que foi removido da steam, mas o player que tava desconectado não teve seu jogo invalidado (o jogo não tinha timestamp e não recebeu estabeleceu a negociação, pois não estava na internet))

No google drive, ele acessa a réplica e envia uma hash de integridade pro cliente. Se a hash n bater, o cliente pede o documento  atualizado. Eu acho que ele separa o documento em chunks para fazer o versionamento (utilizando os diff), pois a chance de a pessoa ter alterado apenas trecho é maior do que ter alterado todo o documento. Ele analisa os metadados de cada chunk e se perceber que houve muitas alterações, o cliente faz a requisição do documento inteiro.

