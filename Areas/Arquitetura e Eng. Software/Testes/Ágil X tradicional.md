---
tipo: conceito
area: Arquitetura e Eng. Software
tags:
- dev/testes
criada: '2024-10-14'
---

## O que é um projeto de software?

Podemos definir um [projeto](obsidian://open?vault=obsidian&file=Areas%2FModelagem%20e%20Desenvolvimento%2FConceitos%20Gerais%2FProjeto%20x%20Processo) de software como sendo um empreendimento temporário dividido em ciclos de vida ou fases com o objetivo de criar um produto, serviço ou resultado único de forma a atender às especificações e expectativas de negócio. Os ciclos de vida de um projeto de software normalmente definem: qual trabalho técnico será realizado, quais entregas serão geradas em cada fase, como serão verificadas e validadas, quais as pessoas ou papéis estarão envolvidos em cada fase e como será realizado o controle e aprovação de cada fase.

Todo o processo de testes, metodologias, equipes e definições são realizados em projetos, por isso é crucial que o conceito esteja claro e bem definido.
## Processo de testes de software

De forma geral, o [processo](obsidian://open?vault=obsidian&file=Areas%2FModelagem%20e%20Desenvolvimento%2FConceitos%20Gerais%2FProjeto%20x%20Processo) de testes de software representa uma estruturação de atividades, etapas, [artefatos](obsidian://open?vault=obsidian&file=Areas%2FArquitetura%20e%20Eng.%20Software%2FTestes%2FConceitos%20gerais%2FArtefatos), papéis e responsabilidades que buscam a padronização de equipes e trabalhos buscando uma forma de ampliar a organização, a qualidade e o controle dos projetos de teste.

Para melhor eficácia e eficiência, o processo de teste, como qualquer outro processo, deve ser revisto continuamente de forma a aperfeiçoar sua atuação buscando a melhoria contínua, além de analisar sua aplicabilidade e continuidade possibilitando aos profissionais envolvidos uma maior visibilidade e organização de seus trabalhos, o que resulta em uma maior agilidade e controle operacional dos projetos.

Independentemente das metodologias utilizadas nos projetos, o processo pode ser dividido em sete partes: planejamento dos testes, especificação dos testes, modelagem dos testes, disponibilização ou preparação do ambiente de testes, execução dos testes, análise dos resultados e encerramento do processo. Segue um breve detalhamento da composição de cada parte:

### Planejamento dos testes

É onde será definido como os testes serão realizados tendo como base as restrições do cliente em relação a prazos, custos e qualidade esperada. Fazem parte das atividades de planejamento: estudar o projeto (quais serão os requisitos, alterações de arquitetura do sistema, avaliar custos, riscos, prazos e impactos), realizar uma análise interna e externa de qual será o esforço (especificar quais serão as métricas utilizadas e fazer uma estimativa do esforço), definir os cenários possíveis (lista de prioridades e riscos), aprovação do planejamento (por meio de aceite da diretoria e dos clientes), definir responsabilidades (qual o papel de cada um no projeto) e mapear os [artefatos](obsidian://open?vault=obsidian&file=Areas%2FArquitetura%20e%20Eng.%20Software%2FTestes%2FConceitos%20gerais%2FArtefatos) (quais serão as documentações e onde será realizada a gestão do projeto).

**Foco Principal:**

- **Definição de como os testes serão realizados, levando em consideração restrições de prazos, custos e qualidade.**

**Atividades Incluídas:**

1. **Estudo do Projeto:**
    - Análise dos requisitos do projeto, alterações na arquitetura do sistema.
    - Avaliação de custos, riscos, prazos e impactos.
2. **Análise de Esforço:**
    - Estimação do esforço necessário, especificação de métricas utilizadas.
    - Realização de análise interna e externa do esforço.
3. **Definição de Cenários Possíveis:**
    - Listagem de prioridades e riscos.
4. **Aprovação do Planejamento:**
    - Obtenção de aceitação da diretoria e dos clientes.
5. **Definição de Responsabilidades:**
    - Atribuição de papéis específicos no projeto.
6. **Mapeamento dos Artefatos:**
    - Definição da documentação necessária e da gestão do projeto.
### Especificação dos testes

Nessa atividade são especificados os cenários e casos de teste considerando os requisitos especificados e a necessidade de cobertura dos testes a serem realizados. Casos de testes são escritos com base em requisitos ou documentos onde estão os critérios de aceite, casos de uso e checklists. Fazem parte das atividades de especificação: estudar os requisitos funcionais e não funcionais e demais documentos solicitados pelos clientes (com o objetivo de entender e identificar inconsistências ou pontos falhos), especificar adaptações da arquitetura dos testes (no que diz respeito às ferramentas utilizadas e exigidas, scripts de testes e de automação), identificar os casos de testes e cenários a serem validados (mapeando fluxos de casos de usos e garantindo que os requisitos estejam totalmente cobertos), refinamento e aceite dos casos de testes (por meio de uma reunião entre a equipe de teste, onde os casos de testes serão apresentados com o objetivo de encontrar pontos de melhoria e garantir a cobertura), definir as responsabilidades (qual o papel de cada membro na equipe de teste) e mapeamento dos [artefatos](obsidian://open?vault=obsidian&file=Areas%2FArquitetura%20e%20Eng.%20Software%2FTestes%2FConceitos%20gerais%2FArtefatos) (qual o padrão de casos de testes, quais ferramentas utilizar, onde reportar bugs).

**Foco Principal:**

- **Identificação e definição de casos de teste e cenários.**
- **Cobertura completa dos requisitos especificados.**

**Atividades Incluídas:**

1. **Estudo dos Requisitos:**
    - Análise dos requisitos funcionais e não funcionais.
    - Identificação de inconsistências ou pontos falhos nos requisitos.
2. **Especificação de Adaptações da Arquitetura dos Testes:**
    - Definição das ferramentas utilizadas, scripts de testes e automação.
3. **Identificação dos Casos de Teste e Cenários:**
    - Mapeamento dos fluxos de casos de uso.
    - Garantia de cobertura completa dos requisitos.
4. **Refinamento e Aceite dos Casos de Teste:**
    - Apresentação e revisão dos casos de teste em reunião da equipe.
    - Identificação de melhorias e garantia de cobertura.
5. **Definição de Responsabilidades:**
    - Atribuição de papéis para cada membro da equipe de teste.
6. **Mapeamento dos Artefatos:**
    - Definição de padrões para casos de teste.
    - Seleção de ferramentas e métodos para reportar bugs.

### Modelagem dos testes

Etapa onde é realizada a definição dos itens necessários para a implementação dos cenários de teste especificados. A tarefa central nessa etapa é a modelagem das massas de testes. Fazem parte das atividades de modelagem: criação dos roteiros de testes (identificação, especificação, organização e revisão dos roteiros e critérios de entrada/saída e de todos os procedimentos para execução dos testes), detalhamento da massa de testes (identificação dos pontos de validação, parametrização, detalhamento da massa de entrada/saída esperada), elaboração do plano de execução dos testes (identificação de quais sistemas estarão envolvidos, quais configurações de hardware, quais características e licenças de uso), quais [artefatos](obsidian://open?vault=obsidian&file=Areas%2FArquitetura%20e%20Eng.%20Software%2FTestes%2FConceitos%20gerais%2FArtefatos) e quais os papéis de cada membro da equipe também fazem parte da modelagem.

**Foco Principal:**

- **Preparação prática para a execução dos testes.**
- **Definição detalhada dos itens necessários para a implementação dos cenários de teste.**

**Atividades Incluídas:**

1. **Criação dos Roteiros de Testes:**
    - Identificação, especificação, organização e revisão dos roteiros.
    - Definição de critérios de entrada/saída e procedimentos de execução.
2. **Detalhamento da Massa de Testes:**
    - Identificação dos pontos de validação e parametrização.
    - Detalhamento da massa de entrada/saída esperada.
3. **Elaboração do Plano de Execução dos Testes:**
    - Identificação dos sistemas envolvidos.
    - Definição das configurações de hardware e características necessárias.
    - Verificação das licenças de uso.
4. **Identificação de Artefatos e Papéis da Equipe:**
    - Detalhamento dos [artefatos](obsidian://open?vault=obsidian&file=Areas%2FArquitetura%20e%20Eng.%20Software%2FTestes%2FConceitos%20gerais%2FArtefatos) a serem utilizados.
    - Clarificação das responsabilidades de cada membro da equipe.

### Disponibilização ou preparação do ambiente de testes

Atividades relacionadas à preparação do ambiente de testes da organização. Fazem parte das atividades de preparação do ambiente: instalação ou atualização do aplicativo a ser testado (atualização do sistema com últimas alterações e implementações, que inclui scripts de banco de dados e códigos fonte), instalação e homologação da arquitetura de testes (caso existam pontos automatizados) e geração da massa de dados (criação via tela, banco de dados ou scripts de um conjunto de informações que possam ser utilizadas para validação das alterações). A definição de papéis de cada membro da equipe de testes também faz parte da preparação do ambiente.

**Foco Principal:**

- **Preparação do ambiente onde os testes serão realizados.**

**Atividades Incluídas:**

1. **Instalação ou Atualização do Aplicativo:**
    - Atualização do sistema com as últimas alterações e implementações, incluindo scripts de banco de dados e códigos fonte.
2. **Instalação e Homologação da Arquitetura de Testes:**
    - Configuração de pontos automatizados, se existirem.
3. **Geração da Massa de Dados:**
    - Criação de um conjunto de informações via tela, banco de dados ou scripts para validação das alterações.
4. **Definição de Papéis da Equipe:**
    - Atribuição de responsabilidades específicas dentro da equipe de testes.
### Execução dos testes

Etapa na qual os testes planejados são executados. Nessa etapa a coleta de [artefatos](obsidian://open?vault=obsidian&file=Areas%2FArquitetura%20e%20Eng.%20Software%2FTestes%2FConceitos%20gerais%2FArtefatos) e informações é importante para a validação plena das funcionalidades, de forma a garantir que os critérios de aceite foram totalmente ou parcialmente cobertos. Fazem parte da execução as seguintes atividades: execução dos casos de testes (seguindo prioridade pré-definida, coleta e análise de evidências, validação de conformidade e não conformidade) e confirmação dos resultados (revalidação das não conformidades e conformidades, análise de impactos). O papel de cada membro dentro da equipe de testes também faz parte da execução dos testes.

**Foco Principal:**

- **Realização prática dos testes planejados e especificados.**

**Atividades Incluídas:**

1. **Execução dos Casos de Teste:**
    - Seguir as prioridades pré-definidas, coleta e análise de evidências, validação de conformidade e não conformidade.
2. **Confirmação dos Resultados:**
    - Revalidação das não conformidades e conformidades, análise de impactos.
3. **Definição de Papéis da Equipe:**
    - Atribuição de responsabilidades específicas dentro da equipe de testes para a execução.

### Análise dos resultados

Nessa atividade os resultados da execução dos testes são comparados com os resultados esperados. Aqueles que não estiverem em conformidade devem ser reportados em detalhes para facilitar a identificação dos defeitos pela equipe de desenvolvimento. Fazem parte das atividades de análise de resultados: revisão dos resultados de não conformidade (avaliar evidências de testes e avaliar e priorizar a lista de bugs), formalizar defeitos encontrados (coletar, detalhar e classificar os defeitos por nível de severidade e priorização), reexecutar testes falhos (avaliar impactos, reexecutar casos de testes com falhas e possíveis casos de sucesso — dependendo da correção, um defeito pode ocasionar outro). Também faz parte da execução dos testes o papel de cada membro dentro da equipe e quais [artefatos](obsidian://open?vault=obsidian&file=Areas%2FArquitetura%20e%20Eng.%20Software%2FTestes%2FConceitos%20gerais%2FArtefatos) serão utilizados como forma de evidenciar os testes executados (como prints de telas, gravação, geração de scripts, passo-a-passo, etc).

**Foco Principal:**

- **Comparação dos resultados da execução dos testes com os resultados esperados e reporte de não conformidades.**

**Atividades Incluídas:**

1. **Revisão dos Resultados de Não Conformidade:**
    - Avaliação de evidências de testes e priorização da lista de bugs.
2. **Formalização dos Defeitos Encontrados:**
    - Coleta, detalhamento e classificação dos defeitos por nível de severidade e priorização.
3. **Reexecução de Testes Falhos:**
    - Avaliação de impactos, reexecução de casos de testes com falhas e possíveis casos de sucesso.
4. **Definição de Papéis da Equipe:**
    - Atribuição de responsabilidades específicas dentro da equipe de testes para a análise.
5. **Coleta de Artefatos:**
    - Evidenciar os testes executados com prints de telas, gravações, geração de scripts, etc.

### Encerramento do processo

Nesta atividade são analisados indicadores extraídos durante a execução dos testes para o trabalho realizado de forma quantitativa e qualitativa. O resultado dessa análise permitirá registrar as lições aprendidas durante a execução dos testes. Fazem parte da atividade de encerramento de processo: extração de indicadores (indicadores quantitativos, de produtividade, confiabilidade, financeiros e de nível de satisfação, individuais e do projeto), resumo do processo de testes (registrar e analisar os indicadores de testes, lista de defeitos, horas planejadas x horas executadas, indicadores de sucesso, lições aprendidas, caminhos críticos e realizar uma divulgação corporativa sobre os resultados obtidos), versionamento dos processos de testes (versionar scripts, casos de testes, ferramentas, códigos fontes utilizados na automação, configurações e ferramentas de produtividade utilizadas), avaliação final e melhoria do processo (avaliar riscos planejados x concretizados, performance, atualizar plano de melhoria contínua e sinalizar o encerramento do processo).

**Foco Principal:**

- **Análise final e documentação das lições aprendidas, além de registrar indicadores de desempenho.**

**Atividades Incluídas:**

1. **Extração de Indicadores:**
    - Coleta de indicadores quantitativos, de produtividade, confiabilidade, financeiros e de nível de satisfação.
2. **Resumo do Processo de Testes:**
    - Registro e análise dos indicadores de testes, lista de defeitos, horas planejadas vs. horas executadas, indicadores de sucesso, lições aprendidas e divulgação dos resultados.
3. **Versionamento dos Processos de Testes:**
    - Versionamento de scripts, casos de testes, ferramentas, códigos fontes utilizados na automação, configurações e ferramentas de produtividade.
4. **Avaliação Final e Melhoria do Processo:**
    - Avaliação de riscos planejados vs. concretizados, performance, atualização do plano de melhoria contínua e sinalização do encerramento do processo.


De um modo geral, de uma metodologia para outra, poucas atividades são alteradas para os testadores. Normalmente o que difere é a ordem e a forma como as atividades são feitas, mas geralmente o processo não sofre alteração na sua essência. As poucas diferenças existentes serão tratadas e exploradas nos tópicos a seguir.

## Testes na Metodologia Tradicional

Nessa metodologia, a atividade de teste é realizada ao final de cada versão, sendo esse o momento em que o analista de testes analisa os requisitos a partir das especificações e das documentações geradas. Entre as atividades de teste podemos destacar:
#### Plano de projeto

Atividade realizada entre o gerente de testes ou outro membro qualificado da equipe e demais gerentes de desenvolvimento, requisitos e o cliente. Esse documento descreverá a aplicação da estratégia de teste no sentido de evidenciar os níveis de teste e especificidades para o projeto em particular.
#### Elaboração do documento de plano de teste

O gerente de teste ou outro membro da equipe qualificado deverá gerar o plano de teste baseando-se nas demandas existentes no plano de projeto, para isso deverá realizar o preenchimento do template ou modelo de plano de teste utilizado pela empresa. Esse modelo deverá conter algumas referências para apoiar o planejamento das atividades. O projeto e plano de testes devem ser criados na ferramenta utilizada pela empresa, a qual pode ser o jira, testlink, mantis, docs, entre outras.
#### Solicitação da validação do documento de plano de teste

O gerente de teste ou o integrante qualificado para tal atividade deverá solicitar a validação do documento de plano de teste. Esse plano deverá ser validado e aprovado pelos [stakeholders](obsidian://open?vault=obsidian&file=Areas%2FModelagem%20e%20Desenvolvimento%2FConceitos%20Gerais%2FStakeholders) e, em casos em que haja necessidade, quando as características do projeto, como complexidade, tamanho e importância, forem críticas, pode-se realizar uma reunião de inspeção em grupo.

#### Avaliação, convocação e solicitação de inspeção em grupo

Essa atividade é orientada por um representante da equipe, intitulado líder de inspeção, que deverá avaliar se a lista de participantes proposta é suficiente para a inspeção e se o prazo entre o envio do material a ser inspecionado e a realização da reunião é suficiente para a preparação dos inspetores. Esse prazo é negociável e fica a cargo dos envolvidos. Para a inspeção é necessário seguir algumas formalidades na convocação dos participantes (nesse caso farão o papel de inspetores), como envio de convites via e-mail contendo a documentação anexa para que os inspetores leiam e avaliem o conteúdo do material, fazendo as anotações, sugestões, dúvidas ou melhorias pertinentes que deverão ser levadas para a reunião, além da data, horário e local da reunião. O objetivo da reunião é encontrar brechas e realizar melhorias e correções no documento, que devem ser feitas pelo gerente. Outra questão importante é manter um histórico de revisão dos documentos e, após as correções e melhorias, os documentos e artefatos gerados devem ser novamente encaminhados aos interessados.
#### Realização da reunião de inspeção

O líder de inspeção e os inspetores se reúnem para discutir o material analisado e decidir qual será o resultado da inspeção. Os resultados, sendo eles sugestões ou alterações, serão registrados em um documento, podendo ser uma planilha de inspeção. Em caso de ausência de algum inspetor, deve-se avaliar a necessidade de cancelamento ou não da inspeção. Faz-se também, nesse caso, o acompanhamento de retrabalho, já que pode ocorrer de a inspeção ter algum documento reprovado. O líder de inspeção deverá acompanhar as correções na documentação. Uma nova reunião também pode ser necessária e deve ser seguido o mesmo padrão para sua convocatória e realização.
#### Criação de cenários de testes

A documentação referente aos cenários de teste deverá ser preenchida conforme obrigatoriedade em um template seguindo um modelo específico. São nos cenários que as condições de teste são identificadas a partir de uma análise sobre os artefatos de especificação (documentos inspecionados nas atividades anteriores, normalmente são documentos de requisitos, casos de uso e/ou especificações funcionais), histórico existente e mesmo experiência do próprio analista de teste envolvido. Com a identificação das condições de teste, é possível agrupá-las de forma a obter uma maior otimização de importância/tempo/recursos na execução dos testes.
#### Criação do plano de teste

Documento que deverá conter as técnicas de teste a serem utilizadas para identificação das condições de teste e cenários de teste. Devem ser avaliadas possíveis fontes de dados existentes relacionadas ao projeto em questão, de forma a complementar os artefatos de especificação existentes. É papel do analista de teste ou do membro experiente na equipe o preenchimento e criação dos planos e cenários de testes, sendo necessário haver posteriormente a inspeção desse documento com a avaliação do analista de requisitos responsável pela documentação do projeto. A inspeção deve seguir o mesmo padrão da atividade relatada anteriormente nos itens “Avaliação, convocação e solicitação de inspeção em grupo” e “Realização da reunião de inspeção”.
#### Criação dos casos de testes

Nessa etapa deve-se utilizar os documentos e artefatos gerados anteriormente, como plano e cenário, e detalhá-los, informando as ações em passos e seus respectivos resultados esperados. A função do analista experiente é realizar uma análise nos documentos de testes com o intuito de escrever o passo-a-passo, contendo título, objetivo, pré-condições, passos e resultados esperados para que os cenários sejam validados. Esses documentos e os casos de testes devem ser armazenados na ferramenta utilizada pela empresa.
#### Revisão e atribuição dos casos de testes

Após os documentos de casos de testes serem concluídos, deve-se avaliar a possibilidade e a necessidade de haver revisão sobre eles para melhorar e analisar se todos os requisitos estão cobertos pelos testes. Havendo a necessidade, pode ser realizada uma reunião de inspeção seguindo também os passos 4 e 5 conforme citado no item “Criação dos casos de testes”, mas nessa etapa o importante seria a participação de todo o time de testes. Concluída a revisão, o caso de teste é atribuído ao responsável por executá-lo no sistema.
#### Execução dos testes

Primeiramente, o membro da equipe responsável pela execução do teste deve avaliar a disponibilidade do ambiente em que serão realizados os testes verificando os requisitos necessários especificados no plano de teste. Deve realizar também a identificação do banco de dados utilizado, informação que também deverá constar no plano de teste. A instalação ou atualização do sistema também é de responsabilidade do executor dos testes, caso não exista uma equipe específica alocada para esse fim. Caso haja alguma automação a ser realizada, ela deverá ser iniciada nessa etapa.
#### Aceite e / ou reprovação dos testes

É papel do testador identificar falhas e erros na execução dos testes, logo eles devem ser executados como consta na especificação. Para isso, o executor ou testador deve acessar a ferramenta utilizada e executar os casos de testes que lhe foram atribuídos, categorizando os resultados obtidos conforme um template, se houver, seguindo um padrão que pode ser: “Teste Passou” - execução sem falha; “Teste Falhou” - execução com falha (obrigatoriamente informando passo a passo resultados esperados e qual a falha); “Bloqueado” - impossibilidade de execução do caso de teste devido a um pré-requisito não atendido ou motivo que não possibilite avaliar o item desejado e “Não executado”. Os defeitos devem ser registrados e notificados aos responsáveis. Em alguns casos, quando são ou não identificados defeitos após o término da execução dos testes, se faz ou não obrigatória a confecção de um documento de comprovação dos testes, ficando a cargo dos envolvidos avaliar sua necessidade. Algumas vezes pode ocorrer de o defeito não ser priorizado ou não fazer parte do escopo inicial das alterações que estavam em teste. Nesses casos devem ser avaliados quais caminhos seguir.

## Testes na Metodologia Ágil

Diferentemente da metodologia tradicional, a atividade de teste no sistema propriamente dito é um processo empírico, sendo realizado em todas as fases do projeto, do início ao fim, onde os profissionais de testes contribuem para o processo como um todo, validando os requisitos desde a sua criação até a entrega final. Como não há necessidade explícita de uma documentação extensa e abrangente, a comunicação entre a equipe é fator crucial de sucesso. Existe a validação de documentos em todos os passos e momentos do processo e isso contribui para o aprendizado de todos, já que todos participam de todo o processo. O analista de teste é responsável por monitorar se as atividades do time estão aderentes ao processo de desenvolvimento além de coletar as métricas do processo de teste.

Entre essas atividades realizadas, podemos destacar:
#### Avaliação da documentação

Com base na documentação ou artefatos é que os profissionais de teste membros do development team irão definir os cenários, fluxos e escrever os casos de testes. Dessa forma, logo que os artefatos forem apresentados, a equipe já deverá trabalhar para validá-los, participando do refinamento e eliminando possíveis brechas, pensando além do descrito nos documentos. Para isso, os testadores devem ler, entender e analisar as user stories. Nessa função deve-se ter sempre em mente a visão do usuário e quais são os possíveis casos reais que ele poderá executar.

**Atividades:**

- **Leitura e Compreensão:** Testadores leem, entendem e analisam as user stories e outros documentos para identificar possíveis brechas e inconsistências.
- **Participação no Refinamento:** Participação ativa no refinamento dos artefatos, contribuindo para a validação e eliminação de possíveis falhas.
- **Visão do Usuário:** Consideração da perspectiva do usuário para prever casos reais de uso e garantir que todos os cenários relevantes sejam cobertos.
#### Criação da documentação de testes

Com os artefatos revisados, melhorados e atualizados, deve-se dar início à escrita de casos de testes. A documentação de testes deve ser simples, direta e clara na medida do possível e deve descrever o passo-a-passo para validação dos critérios de aceite. Fazem parte dessa atividade a criação, manutenção e atualização dos documentos, além da criação de scripts. A documentação normalmente é criada em alguma ferramenta utilizada pela empresa e fica armazenada como histórico, servindo posteriormente como base de testes e criação de templates para funcionalidades mais complexas. Todos na equipe devem ser capacitados para criar a documentação de testes. É uma boa prática sempre realizar uma “validação” dos casos de testes escritos para verificar se a cobertura está completa e/ou se é necessário atualizar, acrescentar ou remover algum teste ou cenário que seja desnecessário. Essa validação pode ser feita por outro membro de testes do development team.

**Atividades:**

- **Criação de Casos de Teste:** Desenvolvimento de documentos que detalham o passo-a-passo para validar funcionalidades.
- **Manutenção e Atualização:** Atualização contínua dos documentos para refletir mudanças e melhorias.
- **Criação de Scripts:** Desenvolvimento de scripts para automação e testes repetitivos.
- **Armazenamento:** Uso de ferramentas específicas para armazenar a documentação, servindo como histórico e base para futuros testes.
- **Validação Cruzada:** Revisão dos casos de teste por outro membro do time para garantir cobertura completa e adequação.
#### Preparação do ambiente de testes

Após os casos de testes e demais artefatos estarem concluídos, os profissionais devem fazer a preparação do ambiente que será utilizado nos testes. Essa preparação poderá incluir a montagem do ambiente, que engloba configuração no banco de dados, instalação e configuração de máquinas virtuais e servidores. Além disso, tem-se também a criação de massa de dados e parametrização no sistema, com o objetivo de deixar o ambiente completo e preparado para receber as atualizações e alterações para o teste. Além dos testadores, pode haver times específicos que trabalham para a disponibilização do ambiente.

**Atividades:**

- **Montagem do Ambiente:** Configuração de banco de dados, máquinas virtuais e servidores.
- **Criação de Massa de Dados:** Geração de dados necessários para simular cenários de teste realistas.
- **Parametrização do Sistema:** Ajustes e configurações no sistema para refletir as condições necessárias para os testes.
- **Colaboração com Outros Times:** Trabalho conjunto com equipes específicas responsáveis pela disponibilização do ambiente de testes.
#### Execução de testes

Após a criação dos casos de testes e demais artefatos, e a verificação de que o ambiente está disponível e com as alterações das user stories aplicadas, os testadores podem iniciar a execução. A instalação ou atualização do sistema pode ser de responsabilidade da equipe de testes caso não exista uma equipe específica alocada para esse fim. Os testes são executados seguindo os artefatos criados e demais documentações. Após a execução, o testador deverá observar se algum outro cenário ou caso não foi coberto pelos artefatos, por isso, testes exploratórios são muito importantes. Sempre deve haver uma boa comunicação entre o time de testes e desenvolvimento dentro do development team, possibilitando a troca de informações, análise do que foi alterado, dúvidas e outras questões que podem ser tratadas.

**Atividades:**

- **Instalação e Atualização:** Implementação de atualizações do sistema, caso não haja uma equipe dedicada a isso.
- **Execução de Casos de Teste:** Realização dos testes conforme documentado.
- **Testes Exploratórios:** Identificação de cenários ou casos não cobertos pelos artefatos documentados.
- **Comunicação Efetiva:** Manutenção de uma boa comunicação entre o time de testes e desenvolvimento para troca de informações e esclarecimento de dúvidas.
#### Aceite e / ou reprovação dos testes

Quando algum comportamento estranho é identificado, é reportado ao desenvolvedor para que possa ser corrigido e depois retestado. Os resultados obtidos também devem ser categorizados conforme um template, se houver, seguindo um padrão, que pode ser: “Teste Passou” - execução sem falha; “Teste Falhou” - execução com falha (onde deve ser informado o passo-a-passo, resultados obtidos e esperados e qual a falha); “Bloqueado” -impossibilidade de execução do caso de teste devido a um pré-requisito não atendido ou motivo que não possibilite avaliar o item desejado e “Não executado”. As user stories somente são aprovadas após todos os defeitos priorizados serem corrigidos e retestados. Após isso, cabe ao product owner e/ou analista funcional realizar o aceite.

**Atividades:**

- **Reportar Comportamentos Estranhos:** Comunicação imediata de falhas ao desenvolvedor para correção.
- **Reteste:** Reavaliação dos testes após correções.
- **Categorização dos Resultados:** Uso de templates para classificar os resultados como “Teste Passou”, “Teste Falhou”, “Bloqueado” ou “Não Executado”.
- **Aprovação das User Stories:** Somente após a correção e reteste de todos os defeitos priorizados, o product owner e/ou analista funcional realiza o aceite final das user stories.


## Diferenças entre as metodologias

	![[Pasted image 20240610164258.png]]

A metodologia tradicional é fundamentada em processos definidos e a metodologia ágil em processos empíricos (observação, experiência e adaptação contínua). De forma mais resumida e direta, podemos observar na **Tabela 1**, e também na **Figura 2**, o que foi discutido até aqui, enfatizando as diferenças e características entre os dois tipos de metodologias, sendo que todos os pontos levantados afetam direta ou indiretamente o processo de testes e a forma sob como e quando são executados.

| METODOLOGIA TRADICIONAL OU CLÁSSICA                                                                                                                                          | METODOLOGIA ÁGIL                                                                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Processos definidos                                                                                                                                                          | Processos empíricos                                                                                                                                              |
| Planejamento rígido                                                                                                                                                          | Maior liberdade no planejamento das ações                                                                                                                        |
| Maior foco em processos do que no produto                                                                                                                                    | Menos formalidade e maior ênfase no produto                                                                                                                      |
| Feedbacks não são essenciais                                                                                                                                                 | Feedbacks são essenciais                                                                                                                                         |
| Documentação extensa                                                                                                                                                         | Documentação necessária                                                                                                                                          |
| Inibe a comunicação entre as pessoas                                                                                                                                         | Estimula a comunicação entre as pessoas                                                                                                                          |
| Planejamento prevê um trabalho extenso, com a entrega do produto somente nos estágios finais do cronograma (não evita conflitos com cliente)                                 | Entregas de partes do projeto de forma contínua e incremental (iterações) com o objetivo de obter um rápido feedback do cliente sobre o andamento do projeto     |
| Conceito de que “entradas iguais sempre geram saídas iguais”                                                                                                                 | Conceito de que “entradas iguais geram saídas diferentes”                                                                                                        |
| Atividades realizadas sequencialmente. Testes executados somente no final, quando “tudo” estiver pronto                                                                      | Atividades realizadas paralelamente. Testes executados durante todo o processo, equipe de testes mais presente em todos os pontos de desenvolvimento             |
| Baseado na definição de todas as etapas do trabalho                                                                                                                          | Baseado na experiência e controlado através de inspeção e adaptação contínua                                                                                     |
| Resistência a mudanças                                                                                                                                                       | Flexibilidade e postura positiva diante da necessidade de mudanças (mesmo em fases finais do projeto)                                                            |
| Decisões tomadas em uma abordagem top-down                                                                                                                                   | Liberdade para o time tomar decisões em conjunto                                                                                                                 |
| Forte centralização em torno da figura do gerente de projetos                                                                                                                | Responsabilidade compartilhada entre os membros da equipe, espírito de colaboração e time engajado                                                               |
| Liderança que monopoliza toda a comunicação já que a preocupação é com o controle das ações                                                                                  | Comunicação fluída e livre entre os membros do time                                                                                                              |
| Líderes indicando “O que fazer” e “Como fazer”, ao invés de dizer o “Porquê”                                                                                                 | Equipes auto-organizáveis; a divisão do trabalho é resultado do entendimento do projeto e de um consenso entre o time                                            |
| Problemas geralmente escalados até a gerência                                                                                                                                | Atuação conjunta do time para a resolução de problemas                                                                                                           |
| Longa fase de análise; em muitos casos parte da equipe é deixada de lado nesses estágios iniciais (já que considera que tais membros ingressarão apenas na fase de execução) | Reuniões diárias entre o time onde são discutidos o que será feito naquele momento, revendo o planejamento a médio e curto prazo, além de prováveis impedimentos |
| Um forte enfoque na geração de documentos e no controle através desses artefatos                                                                                             | Embora existam documentos e se estimule a criação dos mesmos, há um pragmatismo maior (sem conferir uma importância exagerada a esses artefatos)                 |
| Maior envolvimento do cliente em estágios iniciais, com certo relaxamento de postura, uma vez que o projeto tenha se iniciado                                                | Participação ativa do cliente, inclusive enquanto o projeto está sendo implementado                                                                              |
| Foco na “antecipação” (algo difícil em um ambiente sempre sujeito a mudanças repentinas)                                                                                     | Ênfase na “adaptação” (requer “jogo de cintura”)                                                                                                                 |



### Vantagens e desvantagens de cada metodologia

As duas metodologias vistas até aqui, de um modo geral e do ponto de vista do teste, possuem suas vantagens e desvantagens. Agora que já sabemos como é o funcionamento e quais as diferenças entre elas, vamos observar as vantagens e desvantagens da metodologia tradicional e as vantagens e desvantagens da metodologia ágil para então concluirmos em análise, qual delas é viável ou inviável para um determinado projeto.

#### Metodologia Tradicional ou Clássica

| Vantagens                                                                                                                           | Desvantagens                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Torna o processo de desenvolvimento estruturado.                                                                                    | Não fornece feedback entre as fases e não permite a atualização ou redefinição das fases anteriores             |
| Tem uma ordem sequencial de fases. Cada fase cai em cascata na próxima e cada fase deve estar terminada antes do início da seguinte | Não suporta modificações nos requisitos                                                                         |
| Atividades identificadas nas fases do modelo são fundamentais e estão na ordem certa                                                | Não prevê manutenção                                                                                            |
| Fases bem definidas                                                                                                                 | Não permite reutilização                                                                                        |
| Maior foco no planejamento                                                                                                          | É excessivamente sincronizado                                                                                   |
| A fase seguinte só se inicia, geralmente, caso o cliente aceite os artefatos produzidos na fase anterior                            | Se ocorrer um atraso, todo o processo é afetado                                                                 |
|                                                                                                                                     | Exigência de que o cliente estabeleça todos os requisitos no início do projeto                                  |
|                                                                                                                                     | Entrega para a equipe de testes somente próximo ao final do projeto                                             |
|                                                                                                                                     | O modelo conduz a uma rígida divisão de trabalho                                                                |
|                                                                                                                                     | Baixa visibilidade dos problemas                                                                                |
|                                                                                                                                     | Sem status do andamento das atividades para o time                                                              |
|                                                                                                                                     | Entrega para o cliente somente no final do projeto. Não existem entregas parciais                               |
|                                                                                                                                     | Defeitos, erros ou falhas, sejam críticos ou não, são somente encontrados no final. Encarecimento das correções |
|                                                                                                                                     |                                                                                                                 |
#### Metodologia Ágil

| Vantagens                                                                                           | Desvantagens                                                                                                                                    |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Diminuição da expectativa dos clientes por entregas                                                 | Pouca documentação                                                                                                                              |
| Rápida adaptação a mudanças                                                                         | Custo conhecido somente ao longo do projeto. Esse fato exige que o gestor do projeto dedique mais tempo no controle dos custos envolvidos       |
| Maior satisfação dos clientes                                                                       | Manutenção de requisitos requer atenção especial, já que mudanças devem ser acordadas e documentadas                                            |
| Entregas menores, porém com alto valor de negócio para os clientes                                  | Inadequada para projetos com equipes muito grandes. Limita-se o número de membros no time para melhor organização, planejamento e gerenciamento |
| Maior comunicação entre os membros do time                                                          |                                                                                                                                                 |
| Status de cada membro da equipe é transparente aos outros. Todos sabem quais as atividades do outro |                                                                                                                                                 |
| Suporte a modificação de solução e requisitos                                                       |                                                                                                                                                 |
| Todos podem e devem contribuir para o todo. Trabalho em equipe.                                     |                                                                                                                                                 |
| Defeitos, erros ou falhas, sejam críticos ou não, são encontrados durante todo o ciclo              |                                                                                                                                                 |

## Análise comparativa

Já vimos que as metodologias possuem seus pontos altos e baixos, as diferenças entre elas e como funciona o processo de testes dentro de cada uma. Em síntese, todos os modelos assumem que o projeto irá passar por cada etapa apenas uma vez. A diferença é que o ágil preza por uma melhor comunicação, ciclos incrementais, pouca documentação e retrabalho antes da entrega ao cliente e não após a entrega como funciona no modelo tradicional.

A seleção da abordagem mais adequada dependerá de diferentes variáveis, como: características de cada projeto, da empresa e do que é requisitado pelo cliente. Metodologias tradicionais costumam ser mais indicadas em cenários mais formais, além de serem mais recomendadas caso a equipe seja grande e os sistemas a serem desenvolvidos sejam de alto risco (muitas vezes requerem mais documentação). Já métodos ágeis são normalmente mais recomendados para equipes pequenas nas quais a flexibilidade diante de constantes mudanças é fundamental. Embora isso não queira dizer que abordagens ágeis, como o Scrum, não sejam recomendadas para projetos grandes. Vale lembrar que se, na visão do cliente, o produto apenas faz sentido quando for entregue completo, então utilizar métodos ágeis pode não ser a escolha mais adequada.

A escolha da metodologia também deve levar em conta a cultura da empresa, que em situações onde a metodologia ágil pode ser utilizada, não é possível implantá-la, pois o development team não é familiarizado com essa forma de trabalho, com entregas rápidas e percepção de valor antes do produto final. No caso, optar pelo ágil pode aumentar drasticamente os gastos, já que a equipe precisará de treinamento, absorção de conhecimento, além da curva de aprendizado.

Outros fatores que ajudam na escolha da metodologia podem ser: nível de maturidade dos processos na empresa, natureza da aplicação ou sistema, acordos com clientes e tendências de mercado. Cada modelo possui cenários de trabalho diferentes para tratar esses pontos, mas ambos podem ser utilizados. Uma análise de alguns pontos, como o development team, a cultura da empresa, os riscos do projeto, acordos com clientes e gastos, combinados com os pontos positivos e negativos de cada método apresentado devem ajudar a escolher qual a melhor opção.

Existem casos onde, por motivos que levam desde a adaptação até a complexidade do negócio, as duas metodologias podem andar lado a lado, de forma que uma apoie a outra, combinando características das duas metodologias. Pode parecer estranho, mas é muito comum.

Ambas as abordagens são excelentes dentro do que propõem, mas não perfeitas,e possuem pontos altos e baixos em áreas específicas ou em determinados tipos de aplicações utilizadas em projetos distintos.

Ao longo deste artigo, vimos alguns conceitos relativos a processos, desenvolvimento de software, processos de testes, como funcionam as metodologias e como elas podem ajudar ou atrapalhar dependendo do tipo de projeto, analisando suas vantagens e desvantagens.

Definir uma metodologia ou saber como utilizá-la tem fator de importância decisivo entre obter ou não sucesso. Uma má definição ou, ainda, uma má utilização dos recursos providos por elas aumenta consideravelmente os riscos do projeto não obter êxito. Saber utilizar é tão importante quanto a escolha de qual delas utilizar. A definição da metodologia impacta drasticamente na qualidade, já que a equipe de testes é afetada diretamente. Além disso, a escolha da metodologia também afeta a escolha do perfil de profissionais necessários para compor a equipe.

Testes são fundamentais atualmente e fatores como tecnologia, desempenho, performance, rapidez em resposta e qualidade são indispensáveis e devem fazer parte do cotidiano de todos os profissionais e membros do development team. Eles devem ter sempre em mente a intenção de melhoria de qualidade final dos sistemas ou produtos. Toda a equipe deve estar qualificada e engajada no propósito de produzir um produto de confiança e com a velocidade esperada pelos seus clientes. A forma com que isso será feito é onde a metodologia atua.

Criar mais ou menos documentos não é fator decisivo para a escolha de uma metodologia, mas poder opinar, discutir pontos e propor melhorias, sim. Nesse caso, a metodologia tradicional é muito mais engessada do que a ágil, já que a ágil abre espaço a discussões e opiniões de todos os envolvidos, enquanto que na tradicional pouco disso é aproveitado, pois a equipe de testes é tardiamente envolvida.

Mais do que uma mudança, a escolha quebra o paradigma de que só existe uma forma de sucesso para desenvolver e fabricar software. Vimos que tudo depende de vários fatores e, com toda certeza, pode-se ter sucesso tanto com o ágil quanto com o tradicional.

Com diferentes métodos podemos ganhar agilidade, tempo e melhoramos a nossa qualidade nas entregas, mas não garantimos obtenção de sucesso. Para aprimorar a decisão sobre a escolha de métodos, nada melhor do que ter em mente os seguintes pontos: quão receptivos a mudanças são os profissionais que fazem parte da equipe? Qual o acordo sobre entregas com o cliente? Qual nível de exigência do cliente em relação a qualidade? Qual o tamanho da equipe que irá trabalhar no projeto? Qual o nível de conhecimento dos profissionais que fazem parte do time? Qual o risco que se está disposto a assumir para o negócio? Baseado nessas questões e analisando as duas metodologias, conseguimos escolher qual é melhor ou pior para se obter sucesso dentro de um projeto.