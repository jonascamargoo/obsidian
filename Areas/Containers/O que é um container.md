## Definição de virtualização

Virtualização é a tecnologia que permite a criação de ambientes virtuais ou recursos computacionais abstratos, isolados do hardware físico subjacente. Esses ambientes virtuais podem incluir[ máquinas virtuais](obsidian://open?vault=obsidian&file=Areas%2FAOC%2FHierarquia%20de%20mem%C3%B3ria%2FM%C3%A1quina%20Virtual), contêineres ou outros recursos, proporcionando flexibilidade, eficiência e isolamento ao executar múltiplos sistemas operacionais ou aplicativos em um único servidor físico. A virtualização visa otimizar o uso de recursos, melhorar a escalabilidade, facilitar a administração de sistemas e promover a portabilidade de aplicações em ambientes computacionais.

## Definição de container

Container é uma forma avançada de virtualização a nível de sistema operacional, que viabiliza a execução simultânea de múltiplos ambientes isolados dentro de um único sistema operacional hospedeiro - ou seja, mesmo kernel. Essa tecnologia proporciona eficiência e portabilidade ao encapsular aplicativos, bibliotecas e dependências, garantindo que cada contêiner funcione de maneira independente, sem interferir uns nos outros, mesmo compartilhando o mesmo sistema operacional subjacente. Essa abordagem otimizada impulsiona a escalabilidade, facilita a implantação e simplifica a gestão de aplicações em ambientes diversos.

## Kernel modularizado do linux 

"Como o linux possui um kernel todo modularizado, é possível provisionar um sistema muito mais enxuto e barato - por isso é dito virtualização a nível de sistema operacional - diferente de máquinas box por exemplo."

 O kernel do Linux é a parte central do sistema operacional, responsável por gerenciar os recursos do hardware.  "Todo modularizado"  significa que ele é composto por módulos independentes que podem ser carregados e descarregados dinamicamente conforme necessário.

Enquanto as VM tradicionais simulam um SO completo, incluido kernel, os containers só utilizam módulos necessários para seu funcionamento, assim, justificando seu baixo custo relativo.


## Em termos práticos, qual a diferença entre o container e a VM?

Enquanto VMs podem rodar inúmeras coisas, como diferentes linguagens, ambientes de desenvolvimentos, como um SO faz, o container não. A ideia do container é rodar uma única coisa, sendo necessária a orquestração (composição) das partes. Dividindo responsabilidades, isolando processos, sem uma comprometer a outra.






