
Notas sobre a reunião do dia 12/02/2026

Migração de projeto

VLM1 => primeiro filtro macro (retorna um sinal)
VLM 2 etapa -> identifiquei tal empresa. Comparo (veredito -> personificação)

caso carmed e cimed



1 - limpeza dos cadastros (base)
		problema das falsas personificações (camed ta se passando por cimed, mas isso é falso positivo, pois não é fraude)
2 - sistema para detectar atualizações sazonais
3 - geração do cadastro completo para marcas sem site oficial

acessar cimed -> remover asset carmed
tudo no seu devido lugar


Caso do urso por exemplo, não há site para ele (apenas cimed). Então vamos criar uma landpading artificial 

-------------------------------------------------------------

Separou o que tava agrupado e não tinha nada a ver
Até faz sentido (mesmo screenshot), mas não deveriam ta agrupados, pois apesar de ter o mesmo layout, são marcas diferentes

FAZER PRIMEIRO: SE HÁ DOIS CADASTROS DA MESMA MARCA -> JUNTAR
quando tem nome em parenteses, colocar como alias

ajustar os logos quando o logo tiver ruim. Tem cliente que coloca o logo de forma muito cagada (caso sisan consórcio)

Eu devo me guiar pelo html e verificar a situação no pshishdog

FAZER DEPOIS: MAIS DE UMA MARCA DENTRO DE UMA MARCA -> SEPARAR (simpala é uma caso que está certo, separado, branding separado. Seguir modelo dele)

Zoom é outro exemplo (além de sites diferentes, são marcas diferentes. 100% correto)

--------------------------------------------------------------------------------------------------

Pelo annotation, eu acesso cada domínio. Vou no ai-inspection e faço o merge dos que são necessários.



Primeiramente 

COMO JUNTAR
1. definir qual vai ser o principal (qual vai receber os outros)
2. Pega o nome da secundárias e cadastra como alias lá na principal
3. pega o site da secundárias e cadastra como mais um site lá na principal
4. pega os logos da secundárias, baixa e sobe lá na principal
	1. Não esquecer de analisar a qualidade dos logos
	2. Não repetir logos (as vezes o primário já contem o logo do secundário (usar alguma ferramenta para checar similaridade?)
5. salvar o primeiro e deletar o secunário (lembrar de escrever "delete" para deletar de fato, pois tem essa medida de segurança)



## Prompt para dar a tarefa para IA

### Projeto Phishdog (AI-Inspection)

**Contexto do Projeto:** Estou trabalhando na limpeza de dados da plataforma **AI-Inspection (Phishdog)** da Axur. O Phishdog é uma tecnologia de detecção de personificação de marca que usa dois estágios de modelos de visão computacional (VLMs):

1. **VLM1:** Filtro inicial que gera um sinal ao detectar um possível candidato a fraude.
    
2. **VLM2:** Validador que compara o sinal com uma base de dados oficial para confirmar se há personificação real.
    

**O Problema:** A base de dados atual está "suja" devido a falhas na clusterização automática (agrupamento indevido por palavras comuns, como "Café", ou duplicidade de cadastros). Isso gera falsos positivos no VLM2.

**Sua Missão:** Atuar como meu assistente técnico na **Tarefa 1: Limpeza dos Dados**. Eu enviarei o nome de uma marca e alguns links relacionados. Você deve analisar a relação entre eles e me orientar com base nestas diretrizes de negócio:

**Diretrizes de Limpeza (Prioridades):**

1. **JUNTAR (Merge) Primeiro:** Se houver dois cadastros da mesma marca, devemos consolidar em um único cadastro **Principal**.
    
    - O Principal recebe os sites e os nomes das secundárias (nomes em parênteses devem virar **Aliases**).
        
    - Logos da secundária devem ser baixados e subidos na principal apenas se tiverem boa qualidade e não forem repetidos.
        
    - Após migrar tudo, o cadastro secundário deve ser deletado (escrevendo "delete").

**Como vamos interagir:**

- Eu enviarei: **[Marca] + [Links]**.
    
- Você responderá: Uma análise técnica confirmando se os links pertencem à marca, se são sub-marcas (Aliases) ou se são entidades diferentes (Split), sugerindo a ação exata que devo tomar no sistema.
    

A marca atual é esta: "mas money", seu link é [mas.money]. A marcas de possível incidência a serem analisadas são essas:  
1. "Agroenzymas®" - https://agroenzymas.com/
2. "Alianca America Idiomas" - [aliancaamerica.com.br](http://aliancaamerica.com.br/)
3. "Banco Ve Por Más" - [vepormas.com](http://vepormas.com/)
4. "Benteler Sistemas Automotivos" - [benteler.com](http://benteler.com/)


**Entendido? Confirme se compreendeu a lógica do Merge e os conceitos de Brand Name, Aliases e Asset Keys para começarmos.**







--------------------

Notas reuniao dia 10

O motivo real é: Em qual company a IA cadastra o sinal? O mesmo caso as vezes pode cair para um e pode cair para outro 


Notas para a reunião dia 12






ESTUDAR  KNOWLEDGE GRAPH RAGS -> pode ser útil para a área comercial. Já comecei o curso no deeplearning


O website serve para não dar um imperssonation high da própria marca