---
tipo: conceito
area: Banco de dados
tags:
- dados/sql
criada: '2024-10-14'
---

## Descrição

A parte teórica pode ser vista no artigo de [[Álgebra Relacional|Algebra Relacional]] Vamos utilizar um contexto de usuários e artigos associados a cada usuário (1 pra N)

### INNER JOIN:

Retorna apenas os registros que têm correspondência em ambas as tabelas. Ou seja, apenas os registros que atendem à condição de junção são incluídos no resultado.

```sql
SELECT Users.ID, Users.name, Articles.title
FROM Users
INNER JOIN Articles ON Users.ID = Articles.user_id;
```

Neste exemplo, a condição `ON Users.ID = Articles.user_id` especifica que a junção deve ser feita quando o ID de usuário na tabela `Users` for igual ao `user_id` na tabela `Articles`. Somente os registros que têm correspondência nessas duas colunas serão incluídos no resultado.

### LEFT JOIN (ou LEFT OUTER JOIN):

Retorna todos os registros da tabela à esquerda (primeira tabela listada) e os registros correspondentes da tabela à direita (segunda tabela listada). Se não houver correspondência, os valores da tabela à direita serão nulos:

```sql
SELECT Users.ID, Users.name, Articles.title
FROM Users
LEFT JOIN Articles ON Users.ID = Articles.user_id;
```

### RIGHT JOIN (ou RIGHT OUTER JOIN):

Similar ao LEFT JOIN, mas retorna todos os registros da tabela à direita e os registros correspondentes da tabela à esquerda:

```sql
SELECT Users.ID, Users.name, Articles.title
FROM Users
RIGHT JOIN Articles ON Users.ID = Articles.user_id;
```

### FULL JOIN (ou FULL OUTER JOIN):

Retorna todos os registros quando há uma correspondência em qualquer uma das tabelas. Se não houver correspondência, os valores não correspondentes serão nulos.

```sql
SELECT Users.ID, Users.name, Articles.title
FROM Users
FULL JOIN Articles ON Users.ID = Articles.user_id;
```

### Síntese

O uso do operador `JOIN` é fundamental em bancos de dados relacionais para combinar informações de diferentes tabelas com base em relações específicas entre elas. Essas junções permitem consultas complexas que extraem dados inter-relacionados em um único resultado.


