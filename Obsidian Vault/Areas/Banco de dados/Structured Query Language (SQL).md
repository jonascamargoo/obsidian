## O que é?

SQL é a linguagem padrão para interagir com sistemas de gerenciamento de banco de dados relacionais. Os principais tipos de comandos SQL são:

- **Data Definition Language (DDL)**: Comandos para definir a estrutura dos dados: : CREATE, ALTER, DROP, RENAME e TRUNCATE;
- **Data Manipulation Language (DML)**: Comandos para manipulação de dados: INSERT, UPDATE e DELETE;
- **Data Query Language (DQL)**: Comando para consulta de dados: SELECT;
- **Data Transaction Language (DTL)**: Comandos para gerenciar transações: : BEGIN TRANSACTION, COMMIT e ROLLBACK;
- **Data Control Language (DCL)**: Comandos para controle de acesso e permissões: : GRANT e REVOKE.


## Data Definition Language (DDL)

Comandos DDL são usados para definir e alterar a estrutura do banco de dados e seus objetos.

### CREATE: cria novos objetos no BD

``` SQL
-- cria um BD
CREATE DATABASE <banco_de_dados>;

-- cria uma tabela
CREATE TABLE <tabela>(
  <coluna1> <tipo>,
  <coluna2> <tipo>,
  ...
);
```
### DROP: remove objetos do BD

``` SQL
-- remover um banco de dados
DROP DATABASE <banco_de_dados>;

-- remover uma tabela
DROP TABLE <tabela>;
```
### ALTER: altera a estrutura dos objetos do BD

``` SQL
-- Criar uma chave estrangeira para um campo da tabela que faz referência a chave primária de outra tabela
ALTER TABLE <tabel> ADD FOREING KEY <coluna> REFERENCES <tabela> (<coluna>)

-- Adiciona uma coluna
ALTER TABLE <tabela> ADD COLUMN <coluna> <tipo>;

-- Remove uma coluna
ALTER TABLE <tabela> DROP COLUMN <coluna>;

-- Altera o tipo da coluna
ALTER TABLE <tabela> MODIFY COLUMN <coluna> <tipo>;

-- Renomea uma tabela
ALTER TABLE <tabela> RENAME TO <novo_nome>;

-- Adicionar uma chave primária na tabela
ALTER TABLE <tabela> ADD PRIMARY KEY (<coluna>);
```

### RENAME: renomeia um objeto existente no BD

``` SQL  
-- Para renomear um nome de tabela  
RENAME TABLE <nome_atual> TO <novo_nome>;  
  
-- Para renomear uma coluna específica dentro de uma tabela  
ALTER TABLE <tabela> RENAME COLUMN <nome_antigo> TO <novo_nome>;  
```

### TRUNCATE: remove todos os registros de um tabela, mantendo sua estrutura

``` SQL
-- Remover todos registros da tabela sem remover a própria tabela
TRUNCATE TABLE <tabela>;
```


## Data Manipulation Language (DML)

Comandos DML são usados para inserir, atualizar e excluir dados nas tabelas.

### INSERT: adiciona novas linhas a uma tabela

``` SQL
INSERT INTO <tabela>(<coluna1>, <coluna2>, ...) VALUES(valor1, valor2, ...);

INSERT INTO cidade(codCidade, nome) VALUES(1, "Coronel Fabriciano");
INSERT INTO cidade(codCidade, nome) VALUES(2, "Ipatinga"); 
INSERT INTO cidade(codCidade, nome) VALUES(3, "Timóteo"); 
INSERT INTO pessoa(codPessoa, nome, cpf, codCidade) VALUES(1, "Maria", "111.111.111-11", 1);

INSERT INTO pessoa(codPessoa, nome, cpf, codCidade) VALUES(2, "José", "222.222.222-22", 3);

INSERT INTO pessoa(codPessoa, nome, cpf, codCidade) VALUES(3, "Ana", "333.333.333-33", 2);

INSERT INTO pessoa(codPessoa, nome, cpf, codCidade) VALUES(4, "Pedro", "444.444.444-44", 1);
```
### UPDATE: modifica linhas existentes em uma tabela

``` SQL
UPDATE <tabela> SET <coluna1>=valor1, <coluna2>=valor2 WHERE <condição>;
```

### DELETE: remove linhas de uma tabela

``` SQL
DELETE FROM <tabela> WHERE <condição>;

```

OBS: rodar um comando `DELETE` sem a cláusula `WHERE` no MySQL (ou em outros sistemas de gerenciamento de banco de dados relacionais) resultará na exclusão de **todos os registros** da tabela especificada. O comando `DELETE` sem `WHERE` não afeta a estrutura da tabela, apenas remove todos os dados contidos nela.

## Data Query Language (DQL)

Comandos DQL são usados para consultar e recuperar dados do banco de dados.

### SELECT: consulta um conjunto de registros de uma ou mais tabelas

É utilizado para consultar um conjunto de registros (linhas) de uma ou mais tabelas no banco de dados. O comando contém diversas cláusulas, operadores lógicos, relacionais e funções de agregação que permitem filtrar e tratar adequadamente a informação recuperada:

``` SQL
SELECT <coluna1>, <coluna2>, ... FROM <tabela> WHERE <condição>;
SELECT * FROM cidade
SELECT * FROM pessoa;
```


## Data Transaction Language (DTL)

Comandos DTL são usados para gerenciar transações de banco de dados.

* BEGIN TRANSACTION: inicia uma nova transação
* COMMIT: salva todas as mudanças realizadas durante a transação
* ROLLBACK: reverte todas as mudanças realizadas durante a transação

Para iniciar uma transação, você usa o comando `START TRANSACTION` ou `BEGIN`. O comando `BEGIN TRANSACTION` não é padrão SQL e pode não ser suportado por todos os sistemas, mas o `START TRANSACTION` é amplamente aceito:

``` SQL
START TRANSACTION;
-- ou
BEGIN;

-- após iniciar, vamos fazer uma operação qualquer de exemplo:
INSERT INTO Pessoa (codPessoa, nome, cpf, codCidade) VALUES (5, 'Carlos', '555.555.555-55', 1);
UPDATE Pessoa SET nome = 'Carlos Silva' WHERE codPessoa = 5;

-- Agora, vamos confirmar e salvar:
COMMIT;

-- Se ocorrer um erro ou decidir que não devem ser salvas:
ROLLBACK;
```


## Data Control Language (DCL)

A Data Control Language (DCL) é usada para gerenciar permissões e acesso aos dados no banco de dados. Os principais comandos de DCL são:

1. **GRANT**: Concede permissões a usuários:

``` SQL
GRANT <permissão> ON <objeto> TO <usuário>;

-- Exemplo: conceder permissão de 'SELECT' e 'INSERT' na tabela 'Pessoa' ao usuário 'usuario_exemplo'

GRANT SELECT, INSERT ON Pessoa TO 'usuario_exemplo'@'localhost';


```

2. **REVOKE**: Revoga permissões de usuários:

``` SQL
REVOKE <permissão> ON <objeto> FROM <usuário>;

-- Exemplo: revogar a permissão de 'INSERT' na tabela 'Pessoa' do usuário 'usuario_exemplo'

REVOKE INSERT ON Pessoa FROM 'usuario_exemplo'@'localhost';


```

## Principais tipos de dados utilizados em um SGBD

| Tipo                | Descrição                                                                      |
| ------------------- | ------------------------------------------------------------------------------ |
| `INT`               | Inteiro que pode assumir valores de -2147483648 a 2147483647                   |
| `VARCHAR(M)`        | Texto com tamanho máximo de 65535 caracteres                                   |
| `FLOAT(M,D)`        | Ponto flutuante com precisão M e escala D                                      |
| `CHAR(M)`           | Texto que ocupa tamanho fixo entre 0 e 255 caracteres                          |
| `BIGINT`            | Inteiro que pode assumir valores de -9223372036854775808 a 9223372036854775807 |
| `LONGTEXT`          | Texto que permite armazenar até 4.294.967.295 caracteres                       |
| `DECIMAL(M,D)`      | Ponto decimal com M dígitos no total e D casas decimais                        |
| `DATE`              | Data de 01/01/1000 a 31/12/9999 com o formato YYYY-MM-DD                       |
| `TIME`              | Hora no formato HH:MM                                                          |
| `DATETIME`          | Combinação de data e hora                                                      |
| `BOOL` ou `TINYINT` | Valor binário: 0 ou 1                                                          |

## Exemplos

### Exemplo 01

	![[Pasted image 20240726160850.png]]
### Exemplo 02

	Modelo lógico
	Cidade('codCidade', 'nome)
	Pessoa('codPessoa', 'nome', 'cpf', 'codCidade')

``` SQL
-- Criar o banco de dados
CREATE DATABASE Guia01Exemplo01;

-- Selecionar o banco de dados
USE Guia01Exemplo01;

-- Criar a tabela Cidade
CREATE TABLE Cidade(
  codCidade INT,
  nome VARCHAR(255),
  PRIMARY KEY(codCidade)
);

-- Criar a tabela Pessoa
CREATE TABLE Pessoa(
  codPessoa INT,
  nome VARCHAR(5),
  codCidade INT,
  PRIMARY KEY(codPessoa)
);

-- Adicionar chave estrangeira
ALTER TABLE Pessoa ADD FOREIGN KEY (codCidade) REFERENCES Cidade(codCidade);

-- Alterações para corrigir problemas
ALTER TABLE Pessoa ADD COLUMN cpf VARCHAR(14);
ALTER TABLE Pessoa MODIFY COLUMN nome VARCHAR(255);

-- Inserir dados na tabela Cidade
INSERT INTO Cidade(codCidade, nome) VALUES(1, 'Coronel Fabriciano');
INSERT INTO Cidade(codCidade, nome) VALUES(2, 'Ipatinga');
INSERT INTO Cidade(codCidade, nome) VALUES(3, 'Timóteo');

-- Inserir dados na tabela Pessoa
INSERT INTO Pessoa(codPessoa, nome, cpf, codCidade) VALUES(1, 'Maria', '111.111.111-11', 1);
INSERT INTO Pessoa(codPessoa, nome, cpf, codCidade) VALUES(2, 'José', '222.222.222-22', 3);
INSERT INTO Pessoa(codPessoa, nome, cpf, codCidade) VALUES(3, 'Ana', '333.333.333-33', 2);
INSERT INTO Pessoa(codPessoa, nome, cpf, codCidade) VALUES(4, 'Pedro', '444.444.444-44', 1);

-- Consultar todos os registros da tabela Cidade
SELECT * FROM Cidade;

-- Consultar todos os registros da tabela Pessoa
SELECT * FROM Pessoa;

```

### Exemplo 03

	![[Pasted image 20240726165034.png]]


``` sql
create database exemplo03;
use exemplo03;

create table Cliente(
	codCliente int primary key,
	nome varchar(255)
);

create table Produto(
	codProduto int primary key,
	descricao varchar(255),
	valor int
);

create table Pedido(
	numPedido int primary key,
	dataConfirmacao date,
	codCliente int,
	foreign key(codCliente) references Cliente(codCliente)
);

create table PedidoProduto(
	numPedido int,
	codProduto int,
	primary key(numPedido, codProduto),
	quantidade int,
	foreign key(numPedido) references Pedido(codPedido),
	foreign key(numProduto) references Produto(codProduto)
);
```
