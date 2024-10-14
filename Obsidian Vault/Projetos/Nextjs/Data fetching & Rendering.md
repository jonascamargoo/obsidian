## Waterfall vs parallel

Quando precisamos fazer o fetch de alguns dados, podemos fazer isso de forma sequencial ou paralela. A forma sequencial pode ser útil quando um dado depende do outro, porém pode gerar requests waterfall, que é basicamente quando um fetch não consegue avançar pois o anterior não está pronto. Em alguns casos pode ser útil, por exemplo quando precisamos fazer o fetch de um id para então fazer o fetch de um nameById (sem o id não teria como).  Outra opção é realizar o fetch de forma paralela, tendo uma performance bem superior.


## Static and Dynamic Rendering

### Static Rendering

With static rendering, data fetching and rendering happens on the server at build time (when you deploy) or during [revalidation](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating#revalidating-data). The result can then be distributed and cached in a [Content Delivery Network (CDN)](https://nextjs.org/docs/app/building-your-application/rendering/server-components#static-rendering-default).

		![[Pasted image 20240524231330.png]]

Sempre que um usuário visita seu aplicativo, o resultado armazenado em cache é exibido. Existem alguns benefícios da renderização estática:

- Sites mais rápidos – O conteúdo pré-renderizado pode ser armazenado em cache e distribuído globalmente. Isso garante que usuários de todo o mundo possam acessar o conteúdo do seu site de forma mais rápida e confiável;

- Carga reduzida do servidor – Como o conteúdo é armazenado em cache, seu servidor não precisa gerar conteúdo dinamicamente para cada solicitação do usuário;

- SEO - O conteúdo pré-renderizado é mais fácil de ser indexado pelos rastreadores dos mecanismos de pesquisa, pois o conteúdo já está disponível quando a página é carregada. Isso pode levar a melhores classificações nos mecanismos de pesquisa;

- A renderização estática é útil para UI sem dados ou dados compartilhados entre os usuários, como uma postagem de blog estática ou uma página de produto. Pode não ser uma boa opção para um painel que tenha dados personalizados atualizados regularmente.
### Dynamic Rendering


Com a renderização dinâmica, o conteúdo é renderizado no servidor para cada usuário no momento da solicitação (quando o usuário visita a página). Existem alguns benefícios da renderização dinâmica:

- Dados em tempo real - A renderização dinâmica permite que seu aplicativo exiba dados em tempo real ou atualizados com frequência. Isto é ideal para aplicações onde os dados mudam frequentemente;

- Conteúdo específico do usuário – É mais fácil fornecer conteúdo personalizado, como painéis ou perfis de usuário, e atualizar os dados com base na interação do usuário;

- Informações sobre o horário da solicitação - A renderização dinâmica permite acessar informações que só podem ser conhecidas no momento da solicitação, como cookies ou parâmetros de pesquisa de URL.

"With dynamic rendering, **your application is only as fast as your slowest data fetch**." -> lembra o CPU monociclo, que tem o tempo de execução limitado pela instrução mais lenta, não importando o quão rápido são as outras. Imagine um monociclo como uma linha de montagem: cada etapa do processo (buscar instrução, decodificar, buscar dados, executar, escrever resultados) precisa ser concluída antes que a próxima instrução possa iniciar. Se uma etapa leva mais tempo que as outras, toda a linha de montagem fica presa esperando por ela.