

Diretrizes informais podem ser usadas como medidas para determinar a qualidade de projeto. Dentre essas medidas, podemos citar:
* Garantir que a semântica dos atributos seja clara;
* Reduzir a informação redundante nas tuplas;
* Reduzir os valores nulos nas tuplas;
* Prevenir a geração de tuplas falsas.

	![[Pasted image 20240812155547.png]]

## Diretriz 1: Garantir semântica clara dos atributos

Projete um esquema de relação de modo que seja fácil explicar seu significado. Não combine atributos de várias entidades e de relacionamento em uma única relação (NAVATHE, 2011).

Cada tupla de uma relação deve representar uma entidade ou instância de relacionamento. Sendo assim: 

- Atributos de entidades distintas não devem estar na mesma relação 
- Apenas chaves estrangeiras devem ser usadas para referenciar outras entidades 
- Dica: Crie um projeto de esquema que possa ser facilmente explicado. A semântica dos atributos deve ser de fácil interpretação

#### Como não fazer (violação de diretriz)
Entidade com tributos de funcionários e departamentos:

FuncDep(CPF, nomeFunc, dataNasc, endereco, numDep, nomeDep, CPFGerente) 

|           |           |                    |                   |        |               |                |
| --------- | --------- | ------------------ | ----------------- | ------ | ------------- | -------------- |
| CPF       | Nome      | Data de Nascimento | Endereço          | Número | Departamento  | CPF do Gerente |
| 123456789 | Margarida | 22/09/87           | Rua das Flores... | 5      | Pesquisa      | 883024831      |
| 883024831 | Alfredo   | 12/09/69           | Rua da Lapa...    | 5      | Pesquisa      | 883024831      |
| 644494932 | Carla     | 12/12/74           | Av. Ipanema...    | 8      | Administração | 987654311      |
| 987654311 | Ana       | 14/09/87           | Rua Guadalupe...  | 8      | Administração | 987654311      |
| 384949393 | Beatriz   | 16/08/99           | Rua do Horto...   | 1      | RH            | 384949393      |
#### Como fazer

Func(CPF, nomeFunc, dataNasc, endereco, numDep) 

| CPF        | nomeFunc  | dataNasc | Endereco           | numDep |
|-----------|----------|----------|-------------------|-------|
| 123456789  | Margarida | 22/09/87 | Rua das Flores...  | 5     |
| 883024831  | Alfredo   | 12/09/69 | Rua da Lapa...     | 5     |
| 644494932  | Carla     | 12/12/74 | Av. Ipanema...     | 8     |
| 987654311  | Ana       | 14/09/87 | Rua Guadalupe...   | 8     |
| 384949393  | Beatriz   | 16/08/99 | Rua do Horto...    | 1     |

Dep(numDep, nomeDep, CPFGerente)

| numDep | nomeDep       | CPFGerente |
|-------|---------------|------------|
| 5     | Pesquisa      | 883024831  |
| 5     | Pesquisa      | 883024831  |
| 8     | Administração | 987654311  |
| 8     | Administração | 987654311  |
| 1     | RH           | 384949393  |
## Diretriz 2: Reduzir informações redundante nas tuplas

Projete os esquemas de relação de modo que nenhuma anomalia de atualização esteja presente nas relações (NAVATHE, 2011).

Informações redundantes desperdiçam espaço de armazenamento. O agrupamento de atributos de várias entidades pode gerar problemas conhecidos como anomalias de atualização. Estas podem ser classificadas em:

- Anomalias de inserção;
- Anomalias de exclusão ou remoção;
- Anomalias de modificação.

### Anomalias de inserção

Ocorre quando não é possível inserir um novo registro em uma tabela sem inserir informações em outras tabelas relacionadas, mesmo que essas informações não sejam relevantes para o novo registro.

O que acontece se tivermos que inserir um novo funcionário na relação: FuncDep?

| CPF        | nomeFunc | dataNasc | Endereco    | numDep | nomeDep   | CPFGerente |
|-----------|----------|----------|-------------|-------|-----------|------------|
| 222333111  | José     | 18/11/20 | Rua Duque... | 5     | Pesquisa  | 883024831  |
O que acontece se tivermos que inserir um novo departamento na relação: FuncDep?

| CPF        | nomeFunc  | dataNasc | Endereco           | numDep | nomeDep | CPFGerente |
|-----------|----------|----------|-------------------|-------|---------|------------|
|           |          |          |                   | 9     | Vendas  | 883024831  |
### Anomalias de exclusão

Acontece quando a exclusão de um registro em uma tabela leva à exclusão acidental de informações relacionadas em outras tabelas.

O que acontece se tivermos que excluir o último funcionário (Beatriz) de um departamento?

| CPF             | nomeFunc      | dataNasc       | Endereco              | numDep  | nomeDep       | CPFGerente       |
| --------------- | ------------- | -------------- | --------------------- | ------- | ------------- | ---------------- |
| 123456789       | Margarida     | 22/09/87       | Rua das Flores...     | 5       | Pesquisa      | 883024831        |
| 883024831       | Alfredo       | 12/09/69       | Rua da Lapa...        | 5       | Pesquisa      | 883024831        |
| 644494932       | Carla         | 12/12/74       | Av. Ipanema...        | 8       | Administração | 987654311        |
| 987654311       | Ana           | 14/09/87       | Rua Guadalupe...      | 8       | Administração | 987654311        |
| ***384949393*** | ***Beatriz*** | ***16/08/99*** | ***Rua do Horto...*** | ***4*** | ***RH***      | ***384949393***  |

### Anomalias de modificação

Surge quando a atualização de um valor em uma tabela requer a atualização de muitos outros valores em outras tabelas para manter a consistência dos dados.

O que acontece se tivermos que alterar o gerente de um determinado departamento?

| CPF        | nomeFunc  | dataNasc | Endereco           | numDep | nomeDep       | CPFGerente |
|-----------|----------|----------|-------------------|-------|---------------|------------|
| 123456789  | Margarida | 22/09/87 | Rua das Flores...  | 5     | Pesquisa      | 987654311  |
| 883024831  | Alfredo   | 12/09/69 | Rua da Lapa...     | 5     | Pesquisa      | 883024831  |
| 644494932  | Carla     | 12/12/74 | Av. Ipanema...     | 8     | Administração | 987654311  |
| 987654311  | Ana       | 14/09/87 | Rua Guadalupe...   | 8     | Administração | 987654311  |
| 384949393  | Beatriz   | 16/08/99 | Rua do Horto...    | 1     | RH           | 384949393  |

## Diretriz 2: Reduzir os valores nulos nas tuplas


Se possível, evite colocar atributos em uma relação onde os valores podem ser, com frequência, nulos (NAVATHE, 2011).

Um campo com valor nulo pode ter várias interpretações, como:
- O valor não se aplica a tupla. Exemplo: numeroHabilitacao (se pessoa < 18 anos);
- Valor do atributo é desconhecido. Exemplo: certificadoDigital de uma pessoa;
- Valor é conhecido, mas não foi registrado. Exemplo: telefone e endereco

Campos nulos podem causar problemas em operações de junção e cálculos com funções agregadas.

## Diretriz 4: Prevenir a geração de tupla falsa

Projete relações de forma que possam ser unidas utilizando condições de igualdade entre atributos correspondentes (chave primária e chave estrangeira), garantindo que nenhuma tupla falsa seja gerada (NAVATHE, 2011).