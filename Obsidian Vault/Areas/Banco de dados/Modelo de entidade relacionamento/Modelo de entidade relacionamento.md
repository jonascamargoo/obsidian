
Um Modelo de Entidade Relacionamento (MER), também conhecido como Modelo ER, é uma ferramenta gráfica utilizada na área de banco de dados para representar as relações entre diferentes entidades em um sistema. Ele é uma forma de visualizar e projetar a estrutura de um banco de dados antes de sua implementação.

Nesse modelo, as entidades são objetos ou conceitos do mundo real que têm dados armazenados neles. Por exemplo, em um sistema de gerenciamento de biblioteca, as entidades podem incluir "Livro", "Autor" e "Leitor". As relações representam as associações e conexões entre essas entidades.

#### Etapas de um projeto de banco de dados

	1 - Análise e coleta de requisitos: requisitos
	2 - Modelgem: modelagem conceitual
	3 - Mapeamento: mapeamento lógico
	4 - Implementação SGBD: modelo físico

### Os modelos

-  Modelo conceitual
	- **Objetivo:** Representar os requisitos e as relações entre os dados de forma independente de detalhes técnicos.
	- **Atividades:**
	    - Identificação de Entidades: Identificar os principais objetos ou conceitos do sistema como entidades.
	    - Atributos: Identificar os atributos (características) associados a cada entidade.
	    - Relacionamentos: Definir as relações entre as entidades.
	    - Diagrama ER (Entidade-Relacionamento): Representar graficamente as entidades, atributos e relacionamentos
	
- Modelo lógico
	- **Objetivo:** Definir a estrutura e organização dos dados em um nível compreensível para os usuários do sistema de gerenciamento de banco de dados (SGBD).
	- **Atividades:**
	    - Normalização: Aplicar técnicas de normalização para eliminar redundâncias e dependências.
	    - Modelagem de Relacionamento: Refinar os relacionamentos entre as entidades.
	    - Chaves Primárias e Estrangeiras: Definir chaves primárias e estrangeiras para garantir integridade referencial.
	    - Diagrama de Tabelas: Representar as tabelas e seus relacionamentos.
	
- Modelo físico
	- **Objetivo:** Descrever como os dados serão armazenados em disco, incluindo detalhes técnicos.
	- **Atividades:**
	    - Especificação de Tipos de Dados: Definir os tipos de dados a serem utilizados em cada coluna.
	    - Índices: Identificar e criar índices para otimizar consultas.
	    - Particionamento: Dividir grandes conjuntos de dados em partições para melhor desempenho.
	    - Estratégias de Otimização: Implementar estratégias para melhorar o desempenho, como caching, indexing, etc.
	    - Configurações de Armazenamento: Especificar detalhes sobre como os dados serão armazenados fisicamente.



### Modelo conceitual

Foi criada em 1976 por Peter Chen e pode ser considerada a técnica mais difundida e utilizada. O Modelo Entidade Relacionamento (MER) é representado graficamente por um Diagrama Entidade Relacionamento (DER).

- Entidade
	Representa um conjunto de objetos da realidade modelada sobre os quais deseja-se manter informações no banco de dados. Uma entidade pode ser um objeto com uma existência física ou conceitual:
		- Sistema acadêmico: Aluno, Disciplina e Curso;
		- Sistema bancário: Cliente, Conta e Agência.
		
		![[Pasted image 20240308174950.png]]
		Cada retângulo representa um conjunto de objetos sobre os quais deseja-se guardar informações. Caso seja necessário referir um objeto particular (um determinado aluno ou agência) fala-se em ocorrência de entidade (alguns autores usam o termo “instância” de entidade).
		
- Atributo

	Cada entidade possui atributos, ou seja, um conjunto particular de propriedades (características) que a descreve.
	A entidade Aluno pode possuir: nome, CPF, e-mail, número de matrícula, endereço, telefones, data de nascimento, etc. Exemplo: A entidade Aluno pode possuir: nome, CPF, e-mail, número de matrícula, endereço, telefones, data de nascimento, etc:
	
		![[Pasted image 20240308175707.png]]
		
	- Tipos de atributos
		- Simples: não pode ser subdividido
		- Composto: pode ser dividido em partes com significado independente
		- Multivalorado: pode assumir diversos valores em uma mesma ocorrência (instância) da entidade
		- Derivado, calculado ou opcional: pode ser derivado de outros atributos ou entidades relacionadas
		- Chave: atributo onde o valor é utilizado para identificar cada ocorrência da entidade
		
- Relacionamentos

	 Conjunto de associações entre entidades sobre as quais deseja-se manter informações na base de dados.
	 
	 ![[Pasted image 20240308181113.png]]

	 - O relacionamento FAZ é formado por ocorrências das entidades ALUNO e CURSO;
	 - O “grau” de um tipo relacionamento é a quantidade de entidades que participam do relacionamento. No exemplo acima, temos um relacionamento binário, pois duas entidades participam do relacionamento FAZ;
	 - Tipos de relacionamento binários: 
		 - n:n (muitos-para-muitos)
		 - 1:n (um-para-muitos)
		 - 1:1 (um-para-um)
	- Cardinalidade: A cardinalidade de uma entidade em um relacionamento é o número de ocorrências de entidade associadas à uma ocorrência da entidade em questão através do relacionamento. Tipos: Máxima e mínima.
		- Mínima: número mínimo de ocorrências de entidade associadas à uma ocorrência da entidade em questão através do relacionamento. As mais comuns são a "0", que representa opcionalidade e a "1" que representa obrigatoriedade;
		- Máxima: número máximo de ocorrências de entidade associadas à uma ocorrência da entidade em questão através do relacionamento. É utilizada para classificar os relacionamentos: n:n (muitos-para-muitos), 1:1 (um-para-um), 1:n (um-para-muitos).


##### Ainda sobre cardinalidade...

- Tipo de relacionamento 1:1

	![[Pasted image 20240308182936.png]]

Olhando o (1, 1) à direita, percebe-se que cada aluno deve fazer 1 curso no mínimo e 1 curso no máximo. Analisando o parêntese da esquerda, cada curso deve ser feito por 1 no mínimo e por 1 aluno no máximo


	![[Pasted image 20240308183446.png]]

Cada aluno pode ou não fazer um curso. Por outro lado, cada curso deve ser feito por no mínimo 1 aluno e no máximo 1 aluno

	![[Pasted image 20240308184928.png]]

Aqui a opcionalidade reina, ambos podem não ter associado, e no máximo 1. Seria basicamente dizer que "depois de cadastrar olhamos isso, não vamos nos preocupar agora. Cadastra primeiro".

-  Cardinalidade 1:n
	![[Pasted image 20240308185841.png]]


Cada aluno pode se relacionar com no mínimo 1 curso e no máximo com quantos quiser. Cada curso deve estar relacionado a no máx e mín 1 pessoa

![[Pasted image 20240308190243.png]]

Aqui cada aluno pode se relacionar com no máximo n e no mínimo 0. Enquanto cursos podem ser feitos obrigatoriamente por 1 aluno.

- Cardinalidade n:n

	![[Pasted image 20240308190633.png]]

	Aqui cada aluno pode fazer 1 curso no mínimo e quantos quiser no máximo. Cada curso deve ser feito por no mínimo 1 aluno e no máximo por quantos quiser.



## Exercícios

1. Crie um Diagrama de Entidade Relacionamento (DER) para o domínio descrito abaixo:
	Uma biblioteca deseja manter informações sobre seus livros. Para cada livro serão registradas as seguintes
	características: ISBN, título, ano, editora e autores deste livro. Para os autores, deseja manter: nome e
	nacionalidade. É importante ressaltar que um autor pode escrever vários livros, assim como um livro pode
	ser escrito por vários autores. Cada livro da biblioteca pertence a uma categoria. A biblioteca deseja manter
	um cadastro de todas as categorias existentes, com código e descrição. Uma categoria pode ter vários livros
	associados.
	
	Sugestão:
		Identifique as entidades
		Identifique os relacionamentos
		Identifique os atributos para cada entidade
		Identifique o atributo chave de cada entidade