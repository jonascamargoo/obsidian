---
tipo: conceito
area: Banco de dados
tags:
- dados/sql
criada: '2024-10-14'
---

## O que é?

É um modelo matemático que descreve as operações que podem ser realizadas sobre os dados de um banco de dados relacional. A Álgebra Relacional se fundamenta em operadores que atuam sobre relações, permitindo a realização de operações como seleção, projeção, união, interseção, diferença, junção e outras diversas. Essas operações são utilizadas para recuperar, transformar e combinar dados em um banco de dados.

Precisamos definir, primeiramente, o conceito de *tuplas*. No contexto de banco de dados, as tuplas são as linhas da tabela, ou simplesmente "instâncias" de objetos do banco. Por outro lado, as colunas são os atributos de cada instância, ou cada tupla.
## Operações

#### Unárias (sobre uma única relação)

- **Seleção**
- **Projeção**
- **Renomear relação ou atributo**
#### Binárias

- **Produto cartesiano**
- **União**
- **Subtração**
- **Intersecção**
- **Junção**
- **Divisão**
### Sintaxe das Operações

|Operação|Símbolo|Sintaxe|
|---|---|---|
|**Projeção**|π (pi)|π <lista de atributos> (<relação>)|
|**Seleção**|σ (sigma)|σ <condição de seleção> ( <relação> )|
|**Atribuição**|←|R ← (relação)|
|**Renomear**|ρ (rho)|ρ nome (relação)|
|**União**|∪|(relação 1) ∪ (relação 2)|
|**Intersecção**|∩|(relação 1) ∩ (relação 2)|
|**Subtração**|-|(relação 1) - (relação 2)|
|**Produto cartesiano**|×|(relação 1) × (relação 2)|
|**Junção natural**|⨝|(relação 1) ⨝ <condição de junção> (relação 2)|
|**Divisão**|÷|(relação 1) ÷ (relação 2)|

## Modelo

### Modelo conceitual

![[Pasted image 20240726172820.png]]

### Modelo lógico

 **Autor** = (codAutor, nome, dataNascimento, CPF)
**Editora** = (codEditora, nome, CNPJ)
**Livro** = (codLivro, titulo, paginas, ISBN, codEditora)
	codEditora referencia Editora
AutorLivro = (codAutor, codLivro)
	codAutor referencia Autor
    codLivro referencia Livro

### Em tabelas

Utilizarei as tabelas a seguir para exemplo

**Autor**

|codAutor|Nome|dataNascimento|CPF|
|---|---|---|---|
|A1|José|12/10/1980|122.231.123-12|
|A2|Maria|22/05/1990|987.343.321-21|
|A3|Ana|10/08/1988|332.122.897-24|

**Editora**

|codEditora|Nome|CNPJ|
|---|---|---|
|E1|Atlas|91.500.509/0001-59|
|E2|Novatec|83.909.923/0001-98|
|E3|Erica|54.498.944/0001-60|

**Livro**

|codLivro|Titulo|Paginas|ISBN|codEditora|
|---|---|---|---|---|
|L1|Banco de Dados|200|978-85-43025-00-1|E2|
|L2|Programação I|450|978-65-86057-57-7|E3|
|L3|Programação II|150|978-85-5519-321-7|E1|
|L4|Redes de Computadores|700|978-85-5519-356-9|E2|

**AutorLivro**

| codLivro | codAutor |
| -------- | -------- |
| L1       | A1       |
| L1       | A2       |
| L2       | A3       |
| L3       | A3       |
| L4       | A1       |

### Projeção (π)

Produz uma nova relação contendo um subconjunto dos atributos (colunas) da relação argumento. 
A sintaxe é:  π listaAtributos, relação
Exemplo:  `π codAutor, Nome (Autor)`, resulta em:

| codAutor | Nome  |
| -------- | ----- |
| A1       | José  |
| A2       | Maria |
| A3       | Ana   |
### Seleção

- Seleciona tuplas (linhas) da relação que satisfaçam uma ou mais condições.

- Comparadores: <, >, ≤, ≥, =, ≠, ∧ (e lógico), ∨ (ou lógico), ¬ (negação)

- **Sintaxe:** σ <condição de seleção> ( <relação> )

- **Exemplo:** σ codAutor = 'A2' (Autor)

| codAutor | Nome  | dataNascimento | CPF            |
| -------- | ----- | -------------- | -------------- |
| A2       | Maria | 22/05/1990     | 987.343.321-21 |

### Projeção (π) e Seleção (σ)

- Liste o título dos livros da editora E2 que possuem no mínimo 250 páginas.
- **Exemplo:** π titulo (σ paginas > 250 ∧ codEditora = 'E2' (Livro))

| Titulo                |
| --------------------- |
| Redes de Computadores |
### Produto Cartesiano (×)

- Realiza todas as combinações possíveis de tuplas entre duas relações.
- **Sintaxe:** (relação 1) × (relação 2)
- **Exemplo:** Livro × Editora

### Junção (⨝) - Join

- A operação de [junção](obsidian://open?vault=obsidian&file=Areas%2FBanco%20de%20dados%2FJoin)  opera de maneira semelhante à operação de produto cartesiano, mas seu resultado incluirá apenas as combinações das tuplas que se relacionam de acordo com a condição de junção específica. É através dela que criamos uma tabela de relação NxN, chamdas "tabela associativa" (AutorLivro, por exemplo).
- **Sintaxe:** (relação 1) ⨝ <condição de junção> (relação 2)
- **Exemplo:** Livro ⨝ Livro.codEditora = Editora.codEditora Editora

| codLivro | Titulo                | Paginas | ISBN              | codEditora | Nome    | CNPJ               |
| -------- | --------------------- | ------- | ----------------- | ---------- | ------- | ------------------ |
| L1       | Banco de Dados        | 200     | 978-85-43025-00-1 | E2         | Novatec | 83.909.923/0001-98 |
| L2       | Programação I         | 450     | 978-65-86057-57-7 | E3         | Erica   | 54.498.944/0001-60 |
| L3       | Programação II        | 150     | 978-85-5519-321-7 | E1         | Atlas   | 91.500.509/0001-59 |
| L4       | Redes de Computadores | 700     | 978-85-5519-356-9 | E2         | Novatec | 83.909.923/0001-98 |
### União (∪)

- União das tuplas de duas relações, sendo necessário que ambas as relações tenham o mesmo número de atributos e que esses atributos compartilhem o mesmo domínio (tipo). As tuplas duplicadas são eliminadas.
- **Sintaxe:** (relação 1) ∪ (relação 2)
- **Exemplo:** R1 ← π codLivro, titulo (σ paginas < 200 (Livro)), R2 ← π codLivro, titulo (σ paginas > 500 (Livro)), R1 ∪ R2

| codLivro | Titulo                |
| -------- | --------------------- |
| L3       | Programação II        |
| L4       | Redes de Computadores |
#### Intersecção (∩)

- O resultado dessa operação é uma relação que contém as tuplas que estão presentes em ambas as relações.
- **Sintaxe:** (relação 1) ∩ (relação 2)
- **Exemplo:** R1 ← π codLivro, titulo (σ codEditora = 'E2' (Livro)), R2 ← π codLivro, titulo (σ paginas > 250 (Livro)), R1 ∩ R2

| codLivro | Titulo                |
| -------- | --------------------- |
| L4       | Redes de Computadores |
#### Subtração (-)

- Também conhecida como diferença de conjuntos, é uma operação retorna as tuplas que estão presentes em uma relação, mas não estão presentes em outra relação.
- **Sintaxe:** (relação 1) - (relação 2)
- **Exemplo:** R1 ← π codLivro, titulo (Livro), R2 ← π codLivro, titulo (σ codEditora = 'E2' (Livro)), R1 - R2

| codLivro | Titulo         |
| -------- | -------------- |
| L2       | Programação I  |
| L3       | Programação II |
