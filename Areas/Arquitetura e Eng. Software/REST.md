
### Conceito:

Representational State Transfer, abreviado como REST, não é uma tecnologia, uma biblioteca, e nem tampouco uma arquitetura, mas sim um modelo a ser utilizado para se projetar arquiteturas de software distribuído, baseadas em comunicação via rede. O conceito surge da [tese](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm) de doutorado de Roy Fielding, um dos principais criadores do protocolo HTTP.

### ****Identificação dos Recursos****

Todo aplicação gerencia informações. Um banco gerencia clientes, funcionários, contas… essas informações, dentro do REST, são chamadas de recurso. Um recurso nada mais é do que uma abstração sobre um determinado tipo de informação que uma aplicação gerencia, sendo que um dos princípios do REST diz que todo recurso deve possuir uma identificação única. Essa identificação serve para que a aplicação consiga diferenciar qual dos recursos deve ser manipulado em uma determinada solicitação. A identificação do recurso deve ser feita utilizando-se o conceito de URI (Uniform Resource Identifier), que é um dos padrões utilizados pela Web. Alguns exemplos de URIs:

- [http://servicorest.com.br/produtos](http://servicorest.com.br/produtos)
- [http://servicorest.com.br/clientes](http://servicorest.com.br/clientes)
- [http://servicorest.com.br/clientes/57](http://servicorest.com.br/clientes/57)
- [http://servicorest.com.br/vendas](http://servicorest.com.br/vendas)

### URL (uniform resource locator)  vs URI (uniform resource identifier)

Basicamente uma URI identifica e uma URL localiza um recurso, entretanto, localizadores também são identificadores, ou seja, as URLs são um subconjunto do conjunto de URIs

um exemplo de uma URI seria: `cursos.alura.com.br/forum` ela identifica a página do fórum da alura.

agora `https://cursos.alura.com.br/forum` é uma URL pois além de identificar a página do fórum, ela diz também como acessar ele, por meio do protocolo `https`

## Boas práticas no uso das URIs

### Utilizar URIs legíveis

Ao definir uma URI, utilize nomes legíveis por humanos, que sejam de fácil dedução e que estejam relacionados com o domínio da aplicação. Isso facilita a vida dos clientes que utilizarão o serviço, além de reduzir a necessidade de documentações extensas.

### Utilizar mesmo padrão de URIs na identificação dos recursos

Mantenha a consistência na definição das URIs. Crie um padrão de nomenclatura para as URIs dos recursos e utilize sempre esse mesmo padrão. Evite situações como:

- [http://servicorest.com.br/produto](http://servicorest.com.br/produto) (Singular);
- [http://servicorest.com.br/clientes](http://servicorest.com.br/clientes) (Plural);
- [http://servicorest.com.br/processosAdministrativos](http://servicorest.com.br/processosAdministrativos) (Camel Case);
- [http://servicorest.com.br/processos\_judidicais](http://servicorest.com.br/processos/_judidicais) (Snake Case).

### ****Evite adicionar na URI a operação a ser realizada no recurso****

exemplo:

- [http://servicorest.com.br/produtos/cadastrar](http://servicorest.com.br/produtos/cadastrar);
- [http://servicorest.com.br/clientes/10/excluir](http://servicorest.com.br/clientes/10/excluir);
- [http://servicorest.com.br/vendas/34/atualizar](http://servicorest.com.br/vendas/34/atualizar).

### ****Evite adicionar na URI o formato desejado da representação do recurso****

É comum que um serviço REST suporte múltiplos formatos para representar seus recursos, tais como XML, JSON e HTML. A informação sobre qual o formato desejado por um cliente ao consultar um serviço REST deve ser feita via Content Negotiation.

Portanto, evite definir URIs que contenham o formato desejado de um recurso, tais como:

- [http://servicorest.com.br/produtos/xml](http://servicorest.com.br/produtos/xml);
- [http://servicorest.com.br/clientes/112?formato=json](http://servicorest.com.br/clientes/112?formato=json).

### **Evite alterações nas URIs**

A URI é a porta de entrada de um serviço. Se você a altera, isso certamente causará impacto nos clientes que estavam a utilizando, pois você alterou a forma de acesso a ele. Após definir uma URI e disponibilizar a manipulação de um recurso por ela, evite ao máximo sua alteração.

Nos casos mais críticos, no qual realmente uma URI precisará ser alterada, notifique os clientes desse serviço previamente. Verifique também a possibilidade de se manter a URI antiga, fazendo um redirecionamento para a nova URI.

### ****Utilização dos métodos HTTP para manipulação dos recursos****

Quando um cliente dispara uma requisição HTTP para um serviço, além da URI que identifica quais recursos ele pretende manipular, é necessário que ele também informe o tipo de manipulação que deseja realizar no recurso. É justamente aí que entra um outro conceito da Web, que são os métodos do protocolo HTTP: 

[https://www.notion.so/HTTP-146f2b336cf846d7894fbb90b2cb3292#cfa8ebe320cc42ca820e480a0e4aeef8](https://www.notion.so/HTTP-146f2b336cf846d7894fbb90b2cb3292)

## ****Representações dos recursos****

Os recursos ficam armazenados pela aplicação que os gerencia. Quando são solicitados pelas aplicações clientes, por exemplo em uma requisição do tipo GET, eles não "abandonam" o servidor, como se tivessem sido transferidos para os clientes. Na verdade, o que é transferido para a aplicação cliente é apenas uma **representação** do recurso. Um recurso pode ser representado de diversas maneiras, utilizando-se formatos específicos, tais como XML, JSON, HTML, CSV, dentre outros. 

A comunicação entre as aplicações é feita via transferência de representações dos recursos a serem manipulados. Uma representação pode ser também considerada como a indicação do **estado** atual de determinado recurso.

Essa comunicação feita via transferência de representações dos recursos gera um desacoplamento entre o cliente e o servidor, algo que facilita bastante a manutenção das aplicações. 😉 aqui separarmos o client-side do server-side

### **Suporte diferentes representações**

É considerada uma boa prática o suporte a múltiplas representações em um serviço REST, pois isso facilita a inclusão de novos clientes. Ao suportar apenas um tipo de formato, um serviço REST limita seus clientes, que deverão se adaptar para conseguir se comunicar com ele.

Os três principais formatos suportados pela maioria dos serviços REST são:

- HTML;
- XML;
- JSON.

### ****Utilize Content Negotiation para o suporte de múltiplas representações****

Quando um serviço REST suporta mais de um formato para as representações de seus recursos, é comum que ele espere que o cliente forneça a informação de qual o formato desejado. No REST, essa negociação do formato da representação dos recursos é chamada de **Content Negotiation** e no mundo Web ela deve ser feita via um cabeçalho HTTP, conhecido como **accept**.

Ao fazer uma chamada ao serviço REST, um cliente pode adicionar na requisição o cabeçalho accept, para indicar ao servidor o formato desejado da representação do recurso. Claro, deve ser um formato que seja suportado pelo serviço REST.

## ****Comunicação Stateless****

A Web é o principal sistema que utiliza o modelo REST. Hoje ela suporta bilhões de clientes conectados e trocando informações. Mas, como é possível a Web ter uma escalabilidade e performance tão boas, a ponto de conseguir suportar tamanho número de clientes sem problemas? A resposta: Comunicação Stateless!

Clientes não devem depender de dados previamente armazenados no servidor para fazer uma requisição, essas infos devem vir do prórpio cliente, sem sobrecarregar o servidor. Isso reduz a necessidade de grandes quantidades de recursos físicos, como memória e disco, e também melhora a escalabilidade de um serviço REST. É justamente por essa característica que a Web consegue ter uma escalabilidade praticamente infinita, pois ela não precisa manter as informações de estado de cada um dos clientes. 😱 imagine se todos clientes deixassem rastro no servidor de bilhões de clientes?

Esse é um dos princípios mais difíceis de ser aplicado em um serviço REST, pois é muito comum que aplicações mantenham estado entre requisições de clientes. Um exemplo dessa situação acontece quando precisamos armazenar os dados dos usuários que estão autenticados na aplicação.  🤔 se a pessoa ta autenticada no sistema, como saber se ela ta autenticada sem ter representações dela armazenadas no servidor?

### ****Evite manter dados de autenticação/autorização em sessão****

A principal dificuldade em criar um serviço REST totalmente Stateless ocorre quando precisamos lidar com os dados de autenticação/autorização dos clientes. A dificuldade ocorre porque é natural para os desenvolvedores armazenarem tais informações em sessão, pois essa é a solução comum ao se desenvolver uma aplicação Web tradicional.

A principal solução utilizada para resolver esse problema é a utilização de Tokens de acesso, que são gerados pelo serviço REST e devem ser armazenados pelos clientes, via cookies ou HTML 5 Web Storage, devendo também ser enviados pelos clientes a cada nova requisição ao serviço.

Já existem diversas tecnologias e padrões para se trabalhar com Tokens, dentre elas:

- OAUTH;
- JWT (JSON Web Token);
- Keycloack.

QUEM MATÉM O ESTADO É O CLIENTE, NÃO O SERVIDOR!!

## ****HATEOAS (Hypermedia As The Engine Of Application State)****

Vamos supor a seguinte situação: Entro na amazon, quero comprar um produto e clico no menu e vou navegando pelos itens, dai vejo um fora de estoque - o botão de comprar é suspenso pra indicar que ele está indisponível.  O conceito de HATEOAS foi aplicado duas vezes. 

Primeiro, quando o cliente entrou no site de E-commerce, como ele fez para chegar até a página de detalhes do produto? Navegando via **links. N**ormalmente todo site ou aplicação Web possui diversas funcionalidades, sendo que a navegação entre elas costuma ser feita via links. Um cliente até pode saber a URI de determinada página ou recurso, mas se ele não souber precisamos guiá-lo de alguma maneira para que ele encontre as informações que procura. 

O segundo uso do HATEOAS ocorreu quando o cliente acessou a página de detalhes do produto. Se o produto estivesse em estoque, o site apresentaria o botão de comprar, e o cliente poderia finalizar seu pedido. Caso contrário, ele apenas poderia registrar-se para ser notificado. Tudo isso é feito, principalmente, para garantir a consistência das informações.

Perceba que os links foram utilizados como mecanismo para conduzir o cliente quanto à navegação e ao estado dos recursos. Esse é o conceito que foi chamado de HATEOAS, que nada mais é do que a utilização de Hypermedia, com o uso de links, como o motor para guiar os clientes quanto ao estado atual dos recursos, e também quanto as transições de estado que são possíveis no momento.

Veja um exemplo de uma representação de um recurso sem a utilização do conceito de HATEOAS:

<pedido>
    <id>1459</id>
    <data>2017-01-20</data>
    <status>PENDENTE</status>
    <cliente>
         <nome>Rodrigo</nome>
    </cliente>
</pedido>

No exemplo anterior foi apresentado a representação do recurso "Pedido" no formato XML, contendo suas informações, mas sem o uso do HATEOAS. Isso certamente pode gerar algumas dúvidas para os clientes desse serviço REST, como por exemplo:

- É possível solicitar o cancelamento do pedido? Como?
- Quais são os outros estados do pedido e como transitar entre eles?
- Como obter mais informações sobre o cliente desse pedido?

Essas dúvidas poderiam ser respondidas facilmente se o conceito HATEOAS fosse utilizado, facilitando assim a vida dos clientes do serviço REST. Vejamos agora a mesma representação, porém com a utilização do HATEOAS:

```
<pedido self="http://servicorest.com.br/pedidos/1459">
    <id>1459</id>
    <data>2017-01-20</data>
    <status>PENDENTE</status>
    <cliente ref="http://servicorest.com.br/clientes/784" />
    <acoes>
        <acao>
            <rel>self</rel>
            <uri>http://servicorest.com.br/pedidos/1459</uri>
            <method>GET</method>
        </acao>
        <acao>
            <rel>cancelar</rel>
            <uri>http://servicorest.com.br/pedidos/1459</uri>
            <method>DELETE</method>
        </acao>
    </acoes>
</pedido>

```

## Utilização correta dos métodos http

[https://www.notion.so/HTTP-146f2b336cf846d7894fbb90b2cb3292#795617dca96b4ab48e98275ed70dd097](https://www.notion.so/HTTP-146f2b336cf846d7894fbb90b2cb3292)

## Conclusão

REST não é um bicho de sete cabeças. Possui apenas alguns poucos princípios e restrições que devem ser utilizados para se garantir algumas características importantes em aplicações e serviços, tais como: portabilidade, escalabilidade e desacoplamento.

A Web é o principal exemplo de implementação do modelo REST, e deveríamos nos espelhar nela ao construir nossos serviços seguindo esse mesmo modelo.

Todos os conceitos do modelo REST descritos nesse post podem também ser utilizados na implementação de aplicações Web, e não somente nos casos de integração de sistemas via Web Services.

Inclusive se você utilizar esses conceitos em uma aplicação Web tradicional, e um dia ela precisar se tornar uma API REST, o impacto das mudanças será mínimo, pois sua aplicação já estará seguindo os princípios REST. O que mudará é que agora ao invés de devolver para os clientes apenas páginas HTML ela também pode devolver as informações dos recursos em algum formato, como o JSON, e o cliente é quem vai se preocupar em como formatá-los.

Quando uma aplicação ou serviço segue os princípios descritos nesse artigo, ela é chamada de RESTful. Alguns puristas consideram apenas como RESTful a aplicação ou serviço que seguir **todos** os princípios do REST, inclusive os menos utilizados, como comunicação Stateless e HATEOAS.

Mas, não foque em ser ou não considerado RESTful, e sim em tentar utilizar o máximo possível dos princípios REST, para que sua aplicação ou serviço obtenha todos os benefícios desse modelo.

![[restAPI.jpeg]]

Palavras-chave:

portabilidade, escalabilidade e desacoplamento