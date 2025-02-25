
O **Modelo de Entidade-Relacionamento Estendido (EER)**, também conhecido como **Modelo Entidade-Relacionamento Aprimorado**, é uma ferramenta de modelagem de dados que aprimora o modelo original Entidade-Relacionamento (ER) para lidar com situações mais complexas.
## Etapas de um projeto de BD

	![[Pasted image 20240724124259.png]]

LINKAR COM OS CONCEITOS DE MODELO CONCEITUAL, LOGICO, FÍSICO... QUE ESTÃO PRESENTES EM DENTRO DE OUTRO ARQUIVO MD
## Relacionamento

### Autorrelacionamento 

Um relacionamento nem sempre envolve entidades diferentes. Esse é o caso do autorrelacionamento, ou seja, um relacionamento entre instâncias da mesma entidade. Nessa situação, é essencial introduzir um conceito chamado "papel" ou "role", desempenhado pela entidade dentro desse relacionamento. A Figura 2 apresenta um diagrama de ocorrências para o DER da Figura 1:

	![[Pasted image 20240724130623.png]]

	![[Pasted image 20240724130823.png]]

Um exemplo:

	![[Pasted image 20240724130942.png]]


### Relacionamento ternário

São relacionamentos de grau superior a dois, como relacionamentos ternários, quaternários, entre outros. O DER da figura 4 mostra um exemplo de um relacionamento ternário. Veja:

	![[Pasted image 20240724131633.png]]

No caso de relacionamentos de grau maior que dois, o conceito de cardinalidade de relacionamento é uma extensão não trivial do conceito de cardinalidade em relacionamentos binários.
#### Cardinalidade máxima em rel binário
Eem um relacionamento binário R entre duas entidades A e B, a cardinalidade máxima de A em R indica quantas ocorrências de B podem estar associadas a cada ocorrência de A.
#### Cardinalidade máxima em rel ternário
No caso de um relacionamento ternário, a cardinalidade refere-se a pares de entidades. Em um relacionamento R entre três entidades A, B e C, a cardinalidade máxima de A e B dentro de R indica quantas ocorrências de C podem estar associadas a um par de ocorrências de A e B.
#### Exemplo:

Cada par de ocorrências entre cidade e produto está associado, no máximo, a um distribuidor. Portanto, não há concorrência pela distribuição de um produto em uma cidade. Um par de cidade e distribuidor pode estar associado a diversos produtos. Em outras palavras, um distribuidor pode distribuir vários produtos em uma mesma cidade. Um par de produto e distribuidor pode estar associado a várias cidades, ou seja, um distribuidor pode distribuir um mesmo produto em várias cidades:


	![[Pasted image 20240724153656.png]]

	![[Pasted image 20240724154254.png]]



## Entidade associativa

Um relacionamento é uma associação entre entidades. Na modelagem conceitual, normalmente não se permite que uma entidade seja associada diretamente a outro relacionamento, nem que dois relacionamentos sejam conectados entre si. No entanto, ao criar ou modificar um DER, podem surgir situações em que pode ser útil permitir a associação de uma entidade com um relacionamento existente.

### Exemplo

Suponha que seja necessário atualizar o diagrama da Figura 6 para incluir a informação de que, em cada consulta, um ou mais medicamentos podem ser prescritos ao paciente. Para isso, seria criada uma nova entidade chamada MEDICAMENTO. A pergunta que surge é: com qual entidade existente a nova entidade MEDICAMENTO deve ser relacionada?

	![[Pasted image 20240724154927.png]]

Uma entidade associativa nada mais é que a redefinição de um relacionamento, que passa a ser tratado como se fosse uma entidade. Graficamente, isso é feito como mostrado na Figura 7. O retângulo desenhado ao redor do relacionamento CONSULTA indica que este relacionamento passa a ser visto como uma entidade associativa:

	

![[Pasted image 20240724155033.png]]
Caso não seja viável utilizar o conceito de entidade associativa, é possível transformar o relacionamento CONSULTA em uma entidade separada, que pode então ser relacionada com MEDICAMENTO, conforme mostrado na Figura 8:


![[Pasted image 20240724155224.png]]

## Generalização e Especialização

### Conceito
 É um mecanismo que permite agrupar entidades com características comuns em uma entidade mais genérica (superclasse) e, ao mesmo tempo, definir entidades mais específicas (subclasses) que herdam as propriedades da entidade genérica e possuem atributos ou relacionamentos próprios. Associada ao conceito de generalização e especialização está a ideia de herança de propriedades. Herdar propriedades significa que cada ocorrência da entidade especializada possui, além de suas próprias propriedades (atributos e relacionamentos), também as propriedades da ocorrência da entidade genérica correspondente.

### Objetivo
Organizar e hierarquizar as informações, facilitando a representação de classes de objetos com diferentes níveis de abstração.

### Propriedades
**Herança:** Subclasses herdam todos os atributos e relacionamentos da superclasse;
**Especialização:** Subclasses podem possuir atributos e relacionamentos específicos que não existem na superclasse.

### Exemplo
De acordo com o DER da Figura 9, a entidade PESSOA FÍSICA possui seus próprios atributos, como CPF e sexo, bem como todas as propriedades da ocorrência da entidade CLIENTE correspondente. Isso inclui os atributos nome e código, que servem como identificadores, além do relacionamento com a entidade FILIAL.

	![[Pasted image 20240724160131.png]]

### Categorização

A generalização/especialização pode ser categorizada em dois tipos: **total** ou **parcial**, dependendo se é obrigatório ou não que uma ocorrência da entidade genérica corresponda a uma ocorrência da entidade especializada

	![[Pasted image 20240724160938.png]]

Normalmente, quando existe uma especialização **parcial**, na entidade genérica (como no exemplo de FUNCIONÁRIO), é comum utilizar um atributo (tipo de funcionário) que identifique o tipo de ocorrência da entidade genérica.

#### A generalização/especialização também pode ser categorizada em:

**Exclusiva ou Disjunção**: uma ocorrência da entidade genérica é especializada apenas uma vez. Para representar esse tipo de especialização, pode-se utilizar a letra 'x' ou 'd' junto do símbolo.

**Compartilhada ou Sobreposição (Overlap)**: uma ocorrência de uma entidade genérica pode aparecer em várias entidades especializadas. Para representar esse tipo de especialização, pode-se utilizar a letra ‘c’ ou ‘o’ junto com o símbolo:

	![[Pasted image 20240724165135.png]]

## Aplicações, vantagens e desvantagens

### Aplicações do Modelo EER

- Bancos de dados relacionais complexos, como sistemas de e-commerce, gerenciamento de estoque ou bibliotecas.
- Modelagem de sistemas de informação com hierarquias e relações entre entidades.
- Documentação clara e precisa de requisitos de um banco de dados.

### Vantagens do Modelo EER

- Flexibilidade para modelar relacionamentos complexos e hierarquias.
- Maior expressividade do que o modelo ER original.
- Melhora a comunicação entre analistas, desenvolvedores e usuários.
- Facilita a análise e o design de bancos de dados mais robustos.

### Desvantagens do Modelo EER

- Maior complexidade em comparação ao modelo ER básico.
- Pode exigir ferramentas específicas para criação e análise de diagramas EER.
- Implementação em bancos de dados relacionais pode requerer técnicas avançadas.