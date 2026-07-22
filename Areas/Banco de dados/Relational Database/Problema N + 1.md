---
tipo: conceito
area: Banco de dados
tags:
- dados/sql
criada: '2024-10-14'
---

## Definição

O problema N+1 é um padrão antipattern conhecido por ser uma maneira ineficiente de realizar consultas em um banco de dados com um grande volume de dados. Este problema surge quando, ao buscar informações de uma entidade principal (como usuários), são feitas consultas adicionais para obter detalhes relacionados a cada entidade, resultando em um número excessivo de consultas ao banco de dados.
## Exemplo

No exemplo fornecido, considera-se uma situação em que há duas tabelas no banco de dados: uma para usuários e outra para artigos. Existe uma relação de 1 para N entre usuários e artigos, onde N é o número de artigos que cada usuário escreveu. Ao criar um dashboard que exibe dados de todos os usuários e os títulos de seus artigos, o problema N+1 se manifesta da seguinte maneira:

### Consultar todas as informações dos usuários:

`SELECT ID, name, email FROM Users;`
### Em seguida, para cada usuário, consultar os títulos dos artigos:

`SELECT title FROM Articles WHERE user_id = id_usuario;

Se houver 500 usuários, isso resultaria em 501 consultas ao banco de dados, o que pode ter um impacto significativo no desempenho da aplicação. O termo "N+1" reflete o fato de que há uma consulta principal (1) para obter os usuários e, em seguida, uma consulta adicional para cada usuário (N) para obter os artigos relacionados. Ou seja, em uma query eu trago todas as informações sobre os usuários e depois mais 500 para buscar dados associados a cada usuário.

## Como resolver?

### Continuar a consulta que traz os usuários:

```sql
SELECT ID, name, email FROM Users;
```
### Em seguida, utilizar as informações obtidas para fazer uma segunda consulta, onde os artigos são filtrados usando o operador `IN`:

```sql
SELECT title FROM Articles WHERE user_id IN (array_of_users_id);
```

Na nova abordagem proposta, a consulta utiliza a cláusula `IN` para filtrar os resultados com base em uma lista de IDs de usuários. A ideia é fazer uma única consulta para buscar todos os títulos dos artigos relacionados a esses usuários, ao invés de uma consulta para cada usuário separadamente. A consulta ficaria algo assim:

```sql
SELECT title FROM Articles WHERE user_id IN (1, 2, 3, ..., 500);
```

Aqui, `array_of_users_id` seria uma lista contendo os IDs de todos os usuários. Portanto, em vez de realizar 500 consultas individuais, agora você está fazendo apenas uma consulta que busca os títulos dos artigos para todos os usuários de uma vez.
### Analogia

É como se eu ligasse o notebook pra registrar presença (1 query) e fizesse chamada com 30 alunos, um a um (30 queries), totalizando 31 queries. A outra forma seria eu pegar o celular (1 query) e tirasse foto (1 query), totalizando 2 queries com o mesmo resultado.
## Join

O operador [`JOIN`](obsidian://open?vault=obsidian&file=Areas%2FBanco%20de%20dados%2FJoin) em SQL é utilizado para combinar registros de duas ou mais tabelas em uma única consulta, com base em uma condição de relacionamento entre elas. Isso permite extrair informações relacionadas de diferentes tabelas em uma única consulta, facilitando a obtenção de dados complexos de um banco de dados relacional.
### Em vez de usar o operador `IN`, é possível realizar um JOIN entre as tabelas:

```sql
SELECT Users.ID, Users.name, Articles.title
FROM Users
INNER JOIN Articles ON Articles.user_id = Users.ID;
```

O número de consultas pode afetar no desempenho da nossa aplicação, mas isso não significa que por ser 1 consulta será mais eficiente, pois mesmo sendo uma consulta, pode resultar em transferência de dados repetidos. Por exemplo se cada usuário apenas tivesse um artigo escrito, o JOIN seria mais eficiente. Mas se cada usuário tiver em média 5 artigos, teremos muitos dados repetidos trafegando entre o banco de dados e a aplicação, o que pode consumir tempo e memória.