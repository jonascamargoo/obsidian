---
tipo: conceito
area: Banco de dados
tags:
- dados/sql
criada: '2024-10-14'
---

## O que é?

Funções de agregação no SQL são usadas para realizar cálculos em um conjunto de valores e retornar um único valor resumido. Essas funções são extremamente úteis para analisar e resumir dados em tabelas de um banco de dados. Elas são frequentemente usadas em conjunto com a cláusula GROUP BY para agrupar dados antes de aplicar a agregação. As principais funções de agregação são:

- SUM: soma todos os valores;

- AVG: calcula a média dos valores de uma coluna;

- COUNT: conta o número de valores (ou linhas) em uma coluna ou conjunto de colunas;

- MAX: retorna o maior valor em uma coluna;

- MIN: retornar o menor valor em uma coluna..

## Agrupamento de registros

As funções SUM e AVG aceitam apenas conjuntos de números como entrada, enquanto as demais funções podem operar com outros tipos de dados, como texto ou datas. Todas as funções de agregação, exceto COUNT(*), desconsideram colunas com valores NULL ao calcular o resultado. É muito comum utilizar funções agregadas em conjunto com a cláusula GROUP BY, aplicando-as a grupos específicos de dados.

O agrupamento de registros cria subgrupos com base em colunas ou valores retornados por uma expressão. Com a cláusula GROUP BY, é possível agrupar os valores de uma coluna e realizar cálculos sobre esses grupos. Assim, ao executar uma consulta, os valores das linhas são agrupados, permitindo que uma função de agregação seja aplicada a esses grupos.

Frequentemente, é necessário filtrar os dados desses grupos retornados pelo GROUP BY. Para isso, utilizasse a cláusula HAVING, que especifica condições de filtragem em grupos de registros ou agregações. Ela é frequentemente usada em conjunto com o GROUP BY para aplicar filtros nos grupos de dados formados.

*OBS:* o HAVING é bem parecido com a cláusula WHERE, a diferença é que o primeiro condiciona uma coluna a ser calculada (tabela dinâmica resultante, ainda não existente), enquanto a segundo atua em uma coluna física (já existente):

#### HAVING VS WHERE

- **WHERE:**
    - Filtra **linhas individuais** de uma tabela antes do agrupamento.
    - A condição é aplicada a cada linha antes de qualquer cálculo ou agrupamento.
    - Funciona com colunas físicas e existentes na tabela.
- **HAVING:**
    - Filtra **grupos de linhas** criados pela cláusula `GROUP BY`.
    - A condição é aplicada aos resultados dos cálculos de agregação (como `SUM`, `COUNT`, `AVG`, etc.).
    - Funciona com colunas calculadas ou expressões que envolvem funções de agregação.

Imagine uma tabela de vendas com as colunas `produto`, `quantidade` e `valor_total`.

- **WHERE:** Para encontrar todas as vendas de um produto específico, você usaria `WHERE produto = 'X'`.

- **HAVING:** Para encontrar os produtos que geraram um valor total de vendas superior a R$1000, você usaria `GROUP BY produto HAVING SUM(valor_total) > 1000`.

### Sintaxe

``` sql
SELECT , FUNÇÃO_AGREGAÇÃO ( ALL | DISTINCT ) 
FROM <tabelas> 
WHERE <tabela> 
GROUP BY <colunas>
HAVING <condições> 
	ALL: avalia todos os registros (comportamento padrão) DISTINCT: usa apenas valores distintos (sem repetição)
	DISTINC: usa apenas valores distintos (sem repetição)
```



