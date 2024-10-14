
## Junções entre tabelas

As junções de tabelas podem ser feitas utilizando as cláusulas WHERE ou JOIN, que associam tabelas com base em suas chaves primárias e estrangeiras.

### Inner Join

A cláusula INNER JOIN seleciona apenas os registros com valores correspondentes nas colunas das tabelas relacionadas, incluindo no resultado apenas os registros que possuem correspondência em ambas as tabelas:

	![[Pasted image 20240823170459.png]]

### Left Join

A cláusula LEFT JOIN retorna todos os registros da tabela à esquerda (especificada no JOIN) e os registros correspondentes da tabela à direita. Quando não há correspondência na tabela à direita, os valores são preenchidos com NULL:

	![[Pasted image 20240823170716.png]]

``` sql
SELECT colunas FROM tabela_Esq LEFT JOIN tabela_Dir ON tabela_Esq.coluna = tabela_Dir.coluna;
```


### Right Join

A cláusula RIGHT JOIN é semelhante à LEFT JOIN, mas retorna todos os registros da tabela à direita e os registros correspondentes da tabela à esquerda. Quando não há correspondência na tabela à esquerda, os valores são preenchidos com NULL:

	![[Pasted image 20240823170921.png]]

``` sql
SELECT colunas FROM tabela_Esq RIGHT JOIN tabela_Dir ON tabela_Esq.coluna = tabela_Dir.coluna;
```

## Subconsulta

Uma subconsulta é uma instrução SELECT inserida dentro de outra instrução SELECT. Subconsultas permitem criar instruções complexas a partir de instruções simples, sendo especialmente úteis para selecionar linhas de uma tabela com base em condições dependentes de dados dessa mesma tabela.

### Exemplo:

Quem tem o salário maior que o salário de José? 
	Consulta principal:  Os funcionários têm o salário maior que o salário do José 
	Subconsulta: O salário do José

```sql
SELECT colunas FROM tabela 
WHERE 
	coluna OPERADOR (SELECT coluna FROM tabela)
```


### Condições de comparação

As condições de comparação estão divididas em operadores de uma única linha (>, =, >=, <, <>, <=) e operadores de várias linhas (IN, SOME/ANY, ALL)

- IN: igual a qualquer valor da lista (subconsulta) ;

- SOME ou ANY: compara o valor com cada valor da lista (subconsulta) ;

- ALL: compara o valor com todos os valores retornados pela subconsulta.

### UNION

O operador UNION permite combinar os resultados de duas ou mais consultas. Cada instrução SELECT deve ter o mesmo número de colunas, e os tipos de dados das colunas correspondentes devem ser compatíveis. Para ordenar o resultado de uma operação UNION, a cláusula ORDER BY deve ser aplicada após o último SELECT. No ORDER BY, somente os nomes das colunas do primeiro SELECT podem ser utilizados.

```sql
SELECT declaração_1 UNION [ALL} SELECT declaração_2 UNION [ALL} SELECT declaração_3 ... [ORDER BY colunas]
```

OBS: Por padrão, o operador UNION remove resultados duplicados. Para incluí-los no resultado final, adicione a palavra ALL


### Exercícios

Considerando a seguinte tabela:
	![[Pasted image 20240902131809.png]]

#### 1 - Elabore uma sentença SQL para exibir todas as cidades juntamente com seus respectivos moradores. Inclua na lista também as cidades que não têm moradores:

Primeira forma, considerando a tabela esquerda como funcionários e a direita como cidade:

```sql

SELECT C.codCidade, C.nome, F.nome as funcionario FROM Funcionario AS F RIGHT JOIN Cidade AS C ON C.codCidade = F.codCidadeMora ORDER BY C.nome, F.nome;
```

	![[Pasted image 20240902132752.png]]

Segunda forma, considerando tabela à esquerda como Cidade e direita como Funcionário

```sql
SELECT C.codCidade, C.nome, F.nome as funcionario FROM Cidade AS C LEFT JOIN Funcionario AS F ON C.codCidade = F.codCidadeMora ORDER BY C.nome, F.nome;
```

	![[Pasted image 20240902132858.png]]

#### 2 - Crie uma sentença SQL para exibir apenas o código e o nome das cidades que não possuem moradores:

	![[Pasted image 20240902133126.png]]

```sql
SELECT C.codCidade, C.nome FROM Cidade AS C LEFT JOIN Funcionario AS F ON C.codCidade = F.codCidadeMora WHERE F.nome IS NULL ORDER BY C.nome;
```


#### 3 - Elabore uma sentença SQL para calcular e exibir a quantidade de moradores por cidade. Certifique-se de que as cidades que não têm moradores também estejam incluídas nessa relação:

	![[Pasted image 20240902133327.png]]

```sql
SELECT C.codCidade, C.nome, COUNT(F.codCidadeMora) AS Quantidade FROM Cidade AS C LEFT JOIN Funcionario AS F ON C.codCidade = F.codCidadeMora GROUP BY C.codCidade, C.nome ORDER BY C.nome;
```

#### 4 - Crie uma sentença SQL para exibir todos os funcionários (código e nome) e seus respectivos projetos (código e nome). Certifique-se de que os funcionários que não participam de nenhum projeto também estejam incluídos nessa relação:

	![[Pasted image 20240902133659.png]]

```sql
SELECT F.codFuncionario, F.nome as funcionario, P.codProjeto, P.nome as projeto 
FROM FuncionarioProjeto AS FP 
	RIGHT JOIN Funcionario AS F ON FP.codFuncionario = F.codFuncionario 
	LEFT JOIN Projeto AS P ON FP.codProjeto = P.codProjeto ORDER BY F.nome, P.nome;
```


#### 5 - Elabore uma sentença SQL para exibir a lista dos funcionários que recebem salários acima da média geral da empresa:

```sql
SELECT * FROM Funcionario 
	WHERE salario > (
		SELECT AVG(salario) FROM Funcionario
	);
```

#### 6 - Crie uma sentença SQL para exibir a lista dos funcionários com nome, salário e o cálculo do novo salário, conforme a tabela abaixo. Os resultados devem ser ordenados pelo valor calculado:

| **Ajuste** | **Salário**         |
|------------|---------------------|
| 20%        | Até R$ 2.000,00     |
| 10%        | Acima de R$ 2.000,00|


```sql
SELECT nome, salario, (salario * 1.20) AS novosalario 
FROM Funcionario 
WHERE salario <= 2000

UNION 

SELECT nome, salario, (salario * 1.10) AS novosalario
FROM Funcionario
WHERE salario > 2000
ORDER BY novosalario;
```