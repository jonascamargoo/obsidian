## O que é?

Processo de eliminação de esquemas de relações (tabelas) insatisfatório, decompondo-os através da separação de seus atributos em esquemas de relações menos complexas que satisfazem as propriedades desejadas. A função da normalização é eliminar anomalias.

O processo de normalização conduz um esquema de relação através de uma bateria de testes para certificar se o mesmo está na 1ª, 2ª e 3ª Forma Normal. As três formas normais são baseadas em dependências funcionais dos atributos do esquema de relação.

É possível, em casos específicos, criar uma base normalizada e desnormalizar propositalmente para se ter uma performance melhor. Qual a boa prática então? Criar a base normalizada e explicar o porquê está desnormalizando posteriormente.

## 1ª Forma Normal (1FN)

"O que não cabe na 1ª forma normal, não pode ser chamado de tabela"

Todos os atributos de uma relação devem ser atômicos (indivisíveis), ou seja, não são permitidos atributos multivalorados, atributos compostos ou atributos multivalorados compostos:

	![[Pasted image 20240819161844.png]]
### Passos para colocar a relação na 1FN

- Criar uma nova relação com a chave primária da relação original e atributos para cada componente do atributo multivalorado;
- A chave primária da nova relação é uma chave primária composta por todos os atributos da nova relação (normalmente).


## 2ª Forma Normal (2FN)

#### Qual o objetivo?

Evitar anomalias de inserção, exclusão e atualização.
#### Como funciona?

A 2ª Forma Normal prega o conceito da dependência funcional total. Uma relação está na segunda forma normal quando duas condições são satisfeitas:

1. **Já está na 1ª Forma Normal:** Cada célula contém apenas um valor atômico.
2. **Não possui dependências parciais:** Cada atributo não-chave depende de **toda** a chave primária, e não apenas de parte dela.

**Em outras palavras,** todas as informações em uma linha devem estar diretamente relacionadas a **toda** a chave primária. Isso evita redundâncias e inconsistências nos dados.

**Exemplo:** Se a chave primária de uma tabela for composta por "Número do Pedido" e "Produto", o "Preço do Produto" deve depender de ambos, e não apenas do "Produto".

### Exemplo de tabela problemática

	![[Pasted image 20240819164107.png]]

#### Por que está ruim?

Esse aqui é um exemplo de tabela mal modelada, temos algumas dependências parciais. Horas_trabalho é dependência total, pois depende  tanto de Emp_CPF e Proj_Cod. Olhando para Emp_Nome, vemos uma dependência parcial, pois ela depende apenas de Emp_CPF, não de Proj_Cod. O mesmo para Proj_nome e Proj_Local, ambos dependendo apenas de Proj_Cod. Além disso, podemos ver algumas anomalias como anomalia de exclusão (se deletarmos a Lia do SisCorp o projeto some, pois ela é a única). Anomalia de inserção, pois se eu quiser inserir um novo empregado em um projeto já existente, devo repetir nome do projeto, local do projeto... Redundância! Outro problema, atualizar o projeto 3C, transferindo-o para o RJ - devo alterar duas linhas! Anomalia. Precisa ser normalizada.

#### Como ficaria na 2FN?

![[Pasted image 20240819170458.png]]

As setas indicam as referências!

Se uma relação não está na 2ª Forma Normal, a mesma pode ser normalizada gerando outras relações cujos atributos que não façam parte da chave primária sejam totalmente dependente da mesma, ficando a tabela na 2ª Forma Normal.


## 3ª Forma Normal (3FN)

"Uma relação está na 3FN se e somente se estiver na 2FN e nenhum atributo não-primo (isto é, que não seja membro de uma chave) for transitivamente dependente da chave primária." Lembrando Dependência Transitiva: "ocorre quando uma coluna, além de depender da chave primária de uma tabela, depende de outra coluna ou conjunto de colunas da tabela".

### Exemplo de tabela problemática

	![[Pasted image 20240819171510.png]]

Dep_nome e Dep_Ger ambos só dependem de Dep_cod. Então temos um caso de *Dependência transitiva*. Emp_CPF determina transitivamente Dep_Nome e Dep_Ger, pois Emp_CPF determina Dep_Cod e Dep_Cod determina Dep_nome/Dep_Ger.

#### Por que é ruim?

**Anomalia de inserção**: se eu quiser inserir um próximo do mesmo departamente, terei de repetir informação com o risco de errar, como no exemplo abaixo, onde errei o Dep_Nome:

	![[Pasted image 20240828080808.png]]

**Anomalia de exclusão**: como a Ana é a única do Dep de TI, se eu a excluir, o departamento irá sumir também.

**Anomalia de atualização**: se eu mudar o gerente de dep, eu deveria alterar todas as linhas.

#### Normalizando

Criando novas tabelas onde há dependência transitiva:

	![[Pasted image 20240828081221.png]]

Após a normalização, não temos mais anomalias:

	![[Pasted image 20240828081611.png]]

