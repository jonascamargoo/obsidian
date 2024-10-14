## O conceito de frameworks

Vamos pensar que um **frame** representa a estrutura de uma casa, na qual só existem as paredes de tijolos levantadas ou mesmo um carro somente com a lataria, como vemos nas montadoras. Essas estruturas estão aguardando o desenvolvimento (**work**), que no exemplo da casa, corresponderia à escolha da massa corrida que será colocada nas paredes, as cores das tintas, os tipos de pisos.

## Arquitetura modular

Os projetos em Node.js geralmente são chamados de módulos. Esse termo surgiu do conceito de que o JavaScript trabalha com uma arquitetura modular. E quando criamos um projeto, ou seja, um novo módulo, é comum termos associado a ele um arquivo de configuração, que irá descrever os atributos-chaves, dependências, nome, versão, dentre outras informações fundamentais ao projeto. Estamos falando do arquivo `package.json`

- *name*: é onde você define o nome pelo qual seu módulo será chamado;
- *version*: cada vez que uma atualização do módulo é lançada é atribuído um conjunto de 3 números. os módulos trabalham com três níveis de versionamento seguindo um padrão chamado SemVer (*Semantic Versioning*), ou seja, versionamento semântico, onde 3 números separados por ponto correspondem, respectivamente, aos atributos *Major*, *Minor* e *Patch*. *Patch* está relacionado a uma alteração que não quebra uma funcionalidade anterior e nem adiciona novas. Geralmente é usado para liberar alguma correção de bug. *Minor* é quando adicionamos uma nova funcionalidade, sem quebrar funcionalidades anteriores. *Major* é quando pode ocorrer uma quebra de compatibilidade. Por isso, é importante indicar a versão de forma adequada. Você pode ler mais sobre versionamento semântico [aqui](https://semver.org/lang/pt-BR/);
- *description*: define o que será este módulo. Ideal que seja uma descrição curta e clara sobre o objetivo principal;
- *main*: define o ponto de entrada da aplicação;
- *scripts*: essa sessão tem alguns scripts pré-definidos, mas você também pode definir os seus personalizados. Nesse [link](https://docs.npmjs.com/cli/v8/using-npm/scripts) é possível ter acesso a algumas informações sobre os mesmos;
- *keywords*: é um array de palavras-chave sobre o projeto;
- *author*: são dados de autoria, pode conter nome, e-mail e site;
- *license*: é a licença escolhida para o projeto;
- *dependencies*: define a lista de pacotes necessários para executar seu projeto num ambiente de produção;
- *devDependencies*: define a lista de pacotes necessários para executar o projeto num ambiente de desenvolvimento e testes.


