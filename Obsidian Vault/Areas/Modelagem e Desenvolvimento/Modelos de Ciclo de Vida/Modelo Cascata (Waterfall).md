
Nesse contexto temos a metodologia tradicional, possuindo como técnica ou modelo mais conhecido o modelo clássico ou cascata (waterfall), que também é conhecido como abordagem “top-down”. O modelo foi proposto por Royce em 1970, derivado de modelos industriais de diversos segmentos de engenharias; seu principal objetivo era de estabelecer ordem e padrão em desenvolvimento de software. Foi chamado de desenvolvimento tradicional, pois é a base para diversos modelos utilizados há décadas pela indústria de software e é considerado um modelo rígido de pouca flexibilidade, adaptabilidade e versatilidade, sendo utilizado em projetos de pequeno, médio e grande porte.

Grande parte de seu alto grau de aceitação e utilização está no fato de ser um modelo orientado para documentação, seja ela de qualquer tipo, como textos, representações gráficas, simulação, diagramas, casos de usos, entre outras. A ideia principal dessa metodologia é que o software é construído baseado em uma sequência de fases, sendo que cada uma delas depende da conclusão da outra para ser iniciada, com exceção da primeira, conforme ilustra a figura:


	![[Pasted image 20240318164543.png]]

- No modelo em cascata, as fases do projeto são sequenciais e progressivas, com cada fase dependendo da conclusão da anterior;
- As fases típicas incluem: requisitos, análise, projeto, implementação, testes, implantação e manutenção;
- As principais vantagens incluem simplicidade e clareza na definição de requisitos e processos. No entanto, pode ser inflexível em face de mudanças de requisitos e pode levar a problemas de entrega tardia;
- Este modelo é mais adequado para projetos com requisitos bem definidos e estáveis desde o início;
-  Projetos reais raramente seguem um fluxo sequencial;
- Assume que é possível declarar detalhadamente todos os requisitos antes do início das demais fases do desenvolvimento;
- propagação de erros pelas as fases do processo;
- Uma versão de produção do sistema não estará pronta até que o ciclo do projeto de desenvolvimento chegue ao final, o que pode prejudicar o alinhamento (É importante ter um MVP desde o início).

Os resultados da primeira etapa, da Análise, são concluídos, então a saída “flui” para a segunda etapa, que é a de Projeto. Logo, quando a etapa de Projeto for concluída, sua saída ou resultado “flui” para a seguinte, sendo que uma etapa nunca se inicia antes da etapa anterior ser finalizada. As atividades são agrupadas em tarefas executadas sequencialmente.