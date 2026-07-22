---
tipo: conceito
area: Modelagem e Desenvolvimento
tags:
- dev/modelagem
criada: '2024-10-14'
---

1. **Dirigido por Casos de Uso**:
    
    - No RUP, o desenvolvimento é orientado por casos de uso, que descrevem interações entre o sistema e os usuários. Os casos de uso são utilizados para identificar os requisitos funcionais do sistema e servem como base para o planejamento e organização do projeto.
    - A lista de casos de uso ajuda a entender os requisitos do sistema e guia o desenvolvimento das funcionalidades específicas necessárias.

1. **Centrado na Arquitetura**:
    
    - O RUP coloca um forte foco na arquitetura do sistema desde o início do projeto. Através da análise de requisitos e da definição de casos de uso, é elaborada uma arquitetura que permita a implementação dos requisitos e suporte a evolução futura do sistema.
    - A arquitetura é desenvolvida incrementalmente ao longo das iterações, garantindo que ela seja robusta, flexível e capaz de atender aos requisitos do sistema.

1. **Iterativo e Incremental**:
    
    - O RUP é caracterizado por ser iterativo e incremental. O desenvolvimento é dividido em ciclos de desenvolvimento, nos quais novas características são adicionadas à arquitetura do sistema ou as existentes são corrigidas e refinadas.
    - A cada iteração, o sistema se torna mais completo e mais próximo da forma final, permitindo que os stakeholders forneçam feedback e que ajustes sejam feitos ao longo do processo.

1. **Orientado a Riscos**:
    
    - O RUP é orientado a riscos, priorizando a identificação e mitigação dos elementos de maior risco para o projeto. Por exemplo, os casos de uso críticos são identificados, detalhados e implementados antes dos demais, garantindo que os aspectos mais arriscados sejam abordados desde o início do desenvolvimento.
    - Ao abordar os riscos de forma proativa, o RUP ajuda a reduzir a probabilidade de problemas no decorrer do projeto e a garantir a entrega de um sistema de alta qualidade.

Em resumo, o Rational Unified Process (RUP) é um processo de desenvolvimento de software que se baseia em princípios como direcionamento por casos de uso, foco na arquitetura, abordagem iterativa e incremental, e orientação a riscos para garantir o sucesso do projeto e a qualidade do produto final.

Esse software é comumente utilizado em projetos para softwares de risco e sem tolerância a falhas.

###### Boas práticas

- Desenvolvimento iterativo
- Gerenciamento de requisitos
- Arquiteturas baseadas em componentes
- Modelagem visual do software
- Verificar qualidade de software
- Controle de alterações
###### Fases

1. Concepção
	- O objetivo é estabelecer o business case (primeiro documento relacionado ao tema, criado no pré-projeto) para o sistema; 
	- Deve-se identificar todas as entidades externas (pessoas e sistemas) que vão interagir com o sistema e definir as interações;
	- Portanto, deve-se usar essas informações para avaliar a contribuição do sistema para o negócio;
	- Se a contribuição for pequena, então o projeto poderá ser cancelado depois dessa fase.
	
2. Elaboração
	- As metas são desenvolver uma compreensão do problema dominante; 
	- Estabelecer um framework da arquitetura para o sistema;
	- Desenvolver o plano do projeto;
	- Identificar os maiores riscos do projeto;
	- No fim desta fase, deve ter um modelo de requisitos para o sistema, que pode ser um conjunto de casos de uso da UML, uma descrição da arquitetura ou um plano de desenvolvimento de software.
	
3. Construção
	- Envolve projeto, programação e testes do sistema;
	- Durante a fase, as partes do sistema são desenvolvidas em paralelo e integradas; 
	- Ao final, deve-se ter um sistema de software já funcionando, bem como a documentação associada pronta para ser entregue aos usuários.
	
4. Transição
	- A última fase implica transferência do sistema para o usuário e seu funcionamento no ambiente real;
	- Isso é ignorado na maioria dos modelos de processo, mas é, de fato, uma atividade cara e, às vezes, problemática;
	- Na conclusão desta fase, deve-se ter um sistema de software documentada e funcionando corretamente em seu ambiente operacional.