---
tipo: projeto
area: logos
tags:
- ia/agentes
criada: '2026-07-22'
---

O primeiro modelo detecta a posição geométrica -> aqui temos alto recall e muito falso positivo, qualquer coisa pode ser um logo afinal -> yolo (logo ou background)

o Segundo diz de quem é (um cnn triped loss) 


Lookalike -> equivalente ao single domain name da axur


-----------------------------------------------

Nova fase do projeto: analisar os triggers do logo e ver se vai quebrar alguma coisa,, já que vamos mudar o score de continuo para binário



one.axur.com/brand-protection

exp_detection_triggers ->  automacao, quem criou e as regras. Devo filtrar por trigger_was_active=true, .

trigger_priority -> define a concorrencia entre os processor (qual vai primeiro)


devo fiultrar por logo -> BRAND_LOGO


Tem que ter os dois filtros abaixo (ativo e não deletado)
![[Pasted image 20260625163230.png]]


Ver por exemplo se alguma automação quebra ao detectar logo 100% ou algo nesse sentido.  



Rever a parte da renee aos 40 minutos mais ou menos da apresentação do Artur e relacionar com os posts do dia 26 de junho




##########################

Primeiramente, são 41.442 eventos e epaenas 4.589 regras (estado atual de cada uma). Dessas, 21 passaram no filtro inicial do dataset, porém nunca usaram logo. Portanto, são 4.568 (está no final do notebook - apendice)


Não colocar como done -> salvar id, customer dos 10 achados.





