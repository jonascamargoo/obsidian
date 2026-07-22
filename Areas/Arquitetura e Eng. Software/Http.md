---
tipo: conceito
area: Arquitetura e Eng. Software
tags:
- dev/arquitetura
criada: '2024-10-14'
---

### O que é?

	http é um protocolo de comunicação. Seu domínio pode ter raiz nacionalidade (br), comercial (com), oraganizacional (org) e assim vai, podendo ter subdomínios. O DNS (domain name service) recebe o nome e procura algum ip correspondente (em números) como se fosse um banco de dados. O recurso vem depois do domínio. Com um certificado digital (chave pública), a mensagem é descriptografada com uma chave privada quando chega ao servidor, que recebe o requerimento. URL é o endereço do recurso informático.

- ex de URL: [https://alura.com.br:433/course/introducao-html-css](https://alura.com.br:433/course/introducao-html-css)
    - https (protocolo)
    - https: www (significa que estamos na web)
    - [www.alura.com.br](http://www.alura.com.br/) (domínio)
        - com (comercial)
        - br (Brasil)
    - 433 (porta padrão do https, caso nenhuma seja escrita, ele usará essa)
    - [course/introducao-html-css](https://alura.com.br:433/course/introducao-html-css) (recurso específico a ser requerido ao servidor)
    

## Cookies

Cookies de sessão (Chrome: Configurações -> Privacidade -> Configurações de conteúdo... -> Todos os cookies e dados de site... -> Pesquisar alura)

- São dados de autenticação salvados naquela sessão. Por exemplo, logo no site da alura e nao preciso colocar login e senha a cada página que eu visitar no site. Mas se apagar os cookies eles vão pedir login dnv. É um número. Uma requisição sempre deve ser enviada com todas as informações necessárias, o que faz uma requisição ser sempre independente das demais. O HTTP faz uso de comunicação sem estado (stateless), isto é, a cada nova requisição é necessário passar todas as informações necessárias ao servidor, não podendo ser armazenada após cada sessão Http. 



## Métodos http

GET	             > Obter os dados de um recurso.
POST	     > Criar um novo recurso.
PUT	             > Substituir os dados de um determinado recurso.
PATCH	     > Atualizar parcialmente um determinado recurso.
DELETE	     > Excluir um determinado recurso.
HEAD	     > Similar ao GET, mas utilizado apenas para se obter os cabeçalhos de resposta, sem os dados em si.
OPTIONS     > Obter quais manipulações podem ser realizadas em um determinado recurso.

## Alguns pontos sobre REST

- É trabalhar na web da maneira que ela espeifcica: Recurso (URI), Operações possíveis (métodos, verbos) e a representação (html, xml, json);
- É um padrão arquitetural para comunicaçõs entre aplicações;
- Aproveita da estrutura que o html proporciona;
- Os recursos são definidos via URI;
- Opeações com os métodos do HTTP(GET/POST/PUT/DELETE);
- Cabeçalhos (accept/content-type) para especificar a representação (JSAON. XML...);

### STATEFUL HEADER

- No http2, os headers não são reenviados. Se houve alguma alteração, apenas a alteração é enviada, sem repetir informação
    - Headers Stateful permitem que apenas os cabeçalhos que mudem sejam enviados a cada requisição, economizando muita banda que seriam cabeçalhos repetidos.

### HTTP2 - Server Push

- No http1 o arquivo html era lido requisição por requisição, arquivo.css, arquivo.js... porém no http2, quando a primeira requisição é feita, o servidor já envia todas as próximas necessárias de uma vez só, dai o client já identifica antes de fazer requisições desnecessárias. Assim, carregar a página fazendo com que não seja necessário gastar tempo pedindo todos os outros recursos.

### **HTTP2 - Multiplexação**

- geralmente de 4 a 8 conexões tcp/ip são mantidas abertas durante a conexão entre client e servidor, pois é mais performático do que abrir uma conexao tcp/ip (primeira conexao estabelecida, ainda a nível infra) a cada resquest/response. As respostas são assíncronas, isso siginifica que enquanto to mandando o terceiro request, pode ta chegando o primeiro e por ai vai... tudo paralelamente, em vez de fazer apenas um caminho linear em fila (lento) . Não precisa esperar terminar uma pra começar outra e vice-versa