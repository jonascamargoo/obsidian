---
tipo: conceito
area: Redes
tags:
- redes
criada: '2025-01-10'
---

## Cookie

Cookies são pequenos arquivos de texto armazenados pelo navegador que contêm informações associadas a uma interação específica entre o cliente e o servidor. Seu principal propósito é **manter o estado de uma sessão ou identificar o usuário** em requisições futuras.

Exemplos de usos:

- **Autenticação:** Armazenar tokens de sessão que permitem ao usuário permanecer logado.
- **Personalização:** Salvar preferências, como idioma ou tema escuro.
- **Rastreamento:** Monitorar o comportamento do usuário em sites para fins de análise ou publicidade.

Os cookies são enviados em cada requisição HTTP ao servidor, garantindo que o servidor reconheça o usuário e mantenha a continuidade da interação.

Os cookies permitem que sites monitorem seus usuários e personalizem a experiência com base no comportamento e preferências armazenadas. O processo funciona da seguinte maneira:

1. **Criação do ID e envio do cookie:**
    
    - O cliente faz uma solicitação HTTP ao servidor.
    - O servidor, ao receber a solicitação, cria um **ID único** para o usuário e o armazena no banco de dados.
    - O servidor responde à solicitação com o **ID como um cookie**, utilizando o cabeçalho HTTP `Set-Cookie`.
2. **Armazenamento do cookie no cliente:**
    
    - O navegador do cliente armazena o **ID do cookie** localmente, associando-o ao domínio do site.
3. **Uso do cookie em solicitações subsequentes:**
    
    - Em futuras requisições HTTP ao mesmo domínio, o cliente envia automaticamente o cookie armazenado no cabeçalho HTTP `Cookie`.
    - O servidor, ao receber o cookie, identifica o usuário pelo **ID associado** e realiza ações específicas com base nesse identificador (como personalização, autenticação, etc.).
4. **Cabeçalhos HTTP envolvidos:**
    
    - **Cabeçalho `Set-Cookie` (servidor):** É usado pelo servidor para enviar o cookie ao cliente.
    - **Cabeçalho `Cookie` (cliente):** É usado pelo cliente para enviar o cookie de volta ao servidor.

![[Pasted image 20250110152556.png]]


## Web cache

Cache é um mecanismo que armazena temporariamente conteúdos (como imagens, folhas de estilo, scripts, páginas HTML, etc.) no navegador para reduzir o tempo de carregamento e o consumo de recursos em acessos futuros.

Exemplos de uso

- **Desempenho:** Salvar arquivos estáticos para que o navegador não precise baixá-los novamente em visitas subsequentes.
- **Redução de tráfego:** Minimizar a quantidade de dados transferidos entre o cliente e o servidor.

O cache armazena dados relacionados ao **conteúdo estático** do site, enquanto os cookies armazenam dados relacionados ao **estado da interação ou sessão do usuário**.

## Relação entre Cookies e Cache

Embora sejam distintos, cookies e cache podem trabalhar juntos para melhorar a experiência do usuário. Por exemplo:

1. **Melhorando a Personalização:** Cookies podem armazenar informações sobre as preferências do usuário (como idioma ou layout), enquanto o cache armazena os recursos estáticos necessários para exibir a interface com essas preferências.
    
2. **Eficiência de Requisições:** Enquanto o cache reduz a necessidade de transferir recursos estáticos repetidamente, cookies podem reduzir a necessidade de autenticação repetida ou reconfiguração da experiência.
    
3. **Dependência de Cabeçalhos HTTP:** Ambos são controlados por cabeçalhos HTTP, como `Set-Cookie` (para cookies) e `Cache-Control` (para cache), permitindo ao servidor configurar seu comportamento.

### **Diferenças Fundamentais**

|**Aspecto**|**Cookies**|**Cache**|
|---|---|---|
|**Finalidade**|Armazenar informações do estado do usuário (sessões, preferências, etc.).|Armazenar conteúdo estático para melhorar o desempenho.|
|**Escopo**|Dados enviados ao servidor em cada requisição HTTP.|Dados acessados diretamente pelo navegador (não enviados ao servidor).|
|**Tamanho e Limites**|Pequeno (geralmente até 4 KB por cookie).|Pode ser grande (imagens, vídeos, etc.).|
|**Duração**|Controlada pelo servidor com data de expiração definida no cookie.|Configurada pelo servidor com cabeçalhos como `Cache-Control`.|
|**Tipo de dados**|Strings curtas (ID, sessão, preferências).|Arquivos grandes (imagens, CSS, JavaScript).|

## Exemplo prático

Um e-commerce usa cookies para manter o usuário logado e armazenar o carrinho de compras, enquanto o cache é usado para armazenar imagens de produtos e scripts de carregamento da página. Assim, a próxima visita será mais rápida e o carrinho ainda estará acessível.