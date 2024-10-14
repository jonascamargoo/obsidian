## O que é?

Um trigger é um tipo especial de procedimento armazenado, que é executado sempre que há uma tentativa de modificar os dados de uma tabela que é protegida por ele. Por isso temos:

- **Associados a uma tabela**: os TRIGGERS são definidos em uma tabela específica, que é denominada tabela de TRIGGERS;
- **Chamados Automaticamente**: quando há uma tentativa de inserir, atualizar ou excluir os dados em uma tabela, **e um TRIGGER tiver sido definido na tabela para essa ação específica**, ele será executado automaticamente, não podendo nunca ser ignorado.
- **Não podem ser chamados diretamente**: ao contrário dos procedimentos armazenados do sistema, os disparadores não podem ser chamados diretamente e não passam nem aceitam parâmetros.
- **É parte de uma transação**: o TRIGGER e a instrução que o aciona são tratados como uma única transação, que poderá ser revertida em qualquer ponto do procedimento, caso você queria usar “ROLLBACK”, conceitos que veremos mais a frente.

### Orientações básicas quando estiver usando TRIGGER

As **definições de TRIGGERS** podem conter uma instrução “ROLLBACK TRANSACTION”, mesmo que não exista uma instrução explícita de “BEGIN TRANSACTION”.

Se uma instrução “ROLLBACK TRANSACTION” for encontrada, então toda a transação (o TRIGGER e a instrução que o disparou) será revertida ou desfeita. Se uma instrução no script do TRIGGER seguir uma instrução “ROLLBACK TRANSACTION”, a instrução será executada, então, isso nos obriga a ter uma condição IF contendo uma cláusula RETURN para impedir o processamento de outras instruções.

Não é uma boa prática utilizar “ROLLBACK TRANSACTION” dentro de seus TRIGGERS, pois isso gerará um retrabalho, afetando muito no desempenho de seu banco de dados, pois toda a consistência deverá ser feita quando uma transação falhar, lembrando que tanto a instrução quanto o TRIGGER formam uma única transação. O mais indicado é validar as informações fora das transações com TRIGGER para então efetuar, evitando que a transação seja desfeita.

**Para que um TRIGGER seja disparado, o usuário o qual entrou com as instruções, deverá ter permissão de acessar tanto a entidade e consequentemente ao TRIGGER**.

### Usos e aplicabilidade dos TRIGGERS

- Impor uma integridade de dados mais complexa do que uma restrição CHECK;
- Definir mensagens de erro personalizadas;
- Manter dados desnormalizados;
- Comparar a consistência dos dados – posterior e anterior – de uma instrução UPDATE;

Os TRIGGERS são usados com enorme eficiência para impor e manter integridade referencial de baixo nível, e não para retornar resultados de consultas. A principal vantagem é que eles podem conter uma lógica de processamento complexa.

Você pode usar TRIGGERS para atualizações e exclusões em cascata através de tabelas relacionadas em um banco de dados, impor integridades mais complexas do que uma restrição CHECK, definir mensagens de erro personalizadas, manter dados desnormalizados e fazer comparações dos momentos anteriores e posteriores a uma transação.

Quando queremos efetuar transações em cascata, por exemplo, um TRIGGER de exclusão na tabela PRODUTOdo banco de dados Northwind pode excluir os registros correspondentes em outras tabelas que possuem registros com os mesmos valores de PRODUCTID excluídos para que não haja quebra na integridade, como a dito popular “pai pode não ter filhos, mas filhos sem um pai é raro”.

Você pode utilizar os TRIGGERS para impor integridade referencial da seguinte maneira:

- **Executando uma ação ou atualizações e exclusões em cascata**: A integridade referencial pode ser definida através do uso das restrições FOREIGNKEY e REFERENCE, com a instrução CREATE TABLE. Os TRIGGERS fazem bem o trabalho de checagem de violações e garantem que haja coerência de acordo com a sua regra de negócios. Se você exclui um cliente, de certo, você terá que excluir também todo o seu histórico de movimentações. Não seria boa coisa se somente uma parte desta transação acontecesse.
- **Criando disparadores de vários registros**: Quando mais de um registro é atualizado, inserido ou excluído, você deve implementar um TRIGGER para manipular vários registros.

### CRIANDO TRIGGERS

As TRIGGERS são criadas utilizando a instrução CREATE TRIGGER que especifica a tabela onde ela atuará, para que tipo de ação ele irá disparar suas ações seguido pela instrução de conferência para disparo da ação.

E meio a esses comandos, temos algumas restrições para o bom funcionamento. O SQL Server não permite que as instruções a seguir, sejam utilizadas na definição de uma TRIGGER:

- ALTER DATABASE;
- CREATE DATABASE;
- DISKINIT;
- DISKRESIZE;
- DROP DATABASE;
- LOAD DATABASE;
- LOAD LOG;
- RECONFIGURE;
- REATORE DATABASE;
- RESTORELOG.

Caso você queira determinar referencias que um TRIGGER faz a objetos, execute o procedimento armazenado do sistema sp_depends, criando o seguinte comando da **Figura 1**:

	![[Pasted image 20240912155102.png]]



Para determinar os TRIGGERS existentes em uma específica e suas ações, execute o procedimento armazenado do sistema sp_helptrigger, criando o seguinte comando da **Figura 2:**

	![[Pasted image 20240912155130.png]]


## Como funcionam os TRIGGERS?

Quando incluímos, excluímos ao alteramos algum registro em um banco de dados, são criadas tabelas temporárias que passam a conter os registros excluídos, inseridos e também o antes e depois de uma atualização.

Quando você exclui um determinado registro de uma tabela, na verdade você estará apagando a referência desse registro, que ficará, após o DELETE, numa tabela temporária de nome DELETED. Um TRIGGER implementado com uma instrução SELECT poderá lhe trazer todos ou um número de registro que foram excluídos.

Assim como acontece com DELETE, também ocorrerá com inserções em tabelas, podendo obter os dados ou o número de linhas afetadas buscando na tabela INSERTED.

Já no UPDATE ou atualização de registros em uma tabela, temos uma variação e uma concatenação para verificar o antes e o depois.

De fato, quando executamos uma instrução UPDATE, a “engine” de qualquer banco de dados tem um trabalho semelhante, primeiro exclui os dados tupla e posteriormente faz a inserção do novo registro que ocupará aquela posição na tabela, ou seja, um DELETE seguido por um INSERT. Quando então, há uma atualização, podemos buscar o antes e o depois, pois o antes estará na tabela DELETED e o depois estará na tabela INSERTED.

Nada nos impede de retornar dados das tabelas temporárias (INSERTED, DELETED) de volta às tabelas de nosso banco de dados, mas atente-se, os dados manipulados são temporários assim como as tabelas e só estarão disponíveis nesta conexão. Após fechar, as tabelas e os dados não serão mais acessíveis.

### Trigger insert

De acordo com a sua vontade, um TRIGGER por lhe enviar mensagens de erro ou sucesso, de acordo com as transações. Estas mensagens podem ser definidas em meio a um TRIGGER utilizando condicionais IF e indicando em PRINT sua mensagem personalizada. Por exemplo, vamos criar uma tabela chamada tbl_usuario, com a qual simularemos um cadastro de usuários que você também poderá criar para fazer os seus testes. A cada inserção de novo usuário, podemos exibir uma mensagem personalizada de sucesso na inserção. Na **Figura 3** vemos o código para criar a tabela.

	![[Pasted image 20240912155230.png]]

Após criamos a tabela iremos criar nossa TRIGGER personalizada que nos mostrará uma mensagem personalizada a partir de uma inserção. Observe:

	![[Pasted image 20240912155310.png]]

Assim que começarmos a pular nossa tabela tbl_usuario, a cada registro inserido, o SGBD nos devolverá uma mensagem, caso a inserção seja realizada com sucesso, com base nos registros que são adicionados também a nossa tabela lógica/temporária INSERTED. Na **Figura 5** temos a Mensagem disparada pelo TRIGGER:

	![[Pasted image 20240912155333.png]]

Existem várias outras abordagens para o uso de TRIGGERS com INSERTS, por exemplo, quando se faz um controle de entrada e saídas de produtos, podemos ter um TRIGGER executando a baixa dos produtos no estoque (entrada) diante daqueles que foram solicitados num pedido (saída). O TRIGGER pode automatizar essa rotina.

### Trigger Delete

Podemos usar um TRIGGER para monitorar certas exclusões de registros de acordo com a sua regra de negócios e também para proteger a integridade dos dados em um determinado banco de dados.

Alguns fatos devem ser considerados ao usar TRIGGERS DELETE:

- Quando um registro é acrescentado a tabela temporária DELETED, ele deixa de existir na tabela do banco de dados. Portanto, a tabela DELETED, não apresentará registros em comum com as tabelas do banco de dados;
- É alocado espaço na memória para criar a tabela DELETED, que está sempre em cache;
- Um TRIGGER para uma ação DELETE não é executado para a instrução TRUNCATE TABLE porque a mesma não é registrada no log de transações.


Podemos criar um TRIGGER que não permita a exclusão de usuários de nossa tabela tbl_usuario, da seguinte forma:

	![[Pasted image 20240912155618.png]]

O TRIGGER foi criado com sucesso. Na sequência tentaremos executar uma instrução para excluir o usuário que temos já em nossa tabela:
	![[Pasted image 20240912155651.png]]

### Trigger Update

Partindo então do princípio que uma instrução UPDATE apresenta as duas etapas, as quais já citamos, com ela podemos verificar o antes e o depois, já que os dados estarão disponíveis nas tabelas temporárias DELETED – momento anterior – INSERTED – momento atual, logo após o UPDATE.

![[Pasted image 20240912155729.png]]

A qualquer momento daqui por diante, poderemos então contemplar, sempre que executada uma instrução para atualização de registros, o antes e o depois, o que acabamos de definir no TRIGGER para UPDATE.

Vamos então, executar a instrução para atualizar o único registro que temos então em nossa tabela. Mudemos o nome WAGNER BIANCHI para WAGNER BIANCHI Jr. Veremos então como era o nome antes e como é o nome agora:

	![[Pasted image 20240912155757.png]]


#### ALTER

O comando ALETR dá suporte para a alteração de muitos objetos criados dentro de um banco de dados. Podemos chamar alterar o conteúdo de um TRIGGER facilmente, trocando a palavra CREATE por ALTER e em seguida, executando o comando.

	![[Pasted image 20240912160428.png]]
	![[Pasted image 20240912160445.png]]


## Apagando um Trigger

Caso você queira apagar um TRIGGER do banco de dados, utilize DROP TRIGGER mais o nome do TRIGGER que deseja apagar, como: 

	![[Pasted image 20240912160520.png]]