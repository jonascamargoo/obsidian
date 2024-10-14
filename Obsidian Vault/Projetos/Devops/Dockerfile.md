
## image base

trabalhando algumas bases, como a node 20 e a node 20-alpine

#### multi-state building - construção em várias etapas

O "multi-stage building" é uma característica do Docker que permite construir imagens Docker em várias etapas dentro do mesmo Dockerfile. Isso é útil para reduzir o tamanho final da imagem e melhorar a eficiência do processo de construção.

A ideia principal por trás do multi-stage building é usar diferentes estágios durante o processo de construção da imagem. Cada estágio pode executar tarefas específicas, como compilação de código, instalação de dependências, entre outras, e os resultados dessas etapas anteriores podem ser usados em estágios posteriores.

Por exemplo, imagine que você esteja construindo uma aplicação que requer uma etapa de compilação para transformar o código-fonte em um executável e outra etapa para empacotar esse executável em uma imagem final. Com o multi-stage building, você pode definir um estágio inicial para compilar o código-fonte e outro estágio para criar a imagem final usando o resultado da compilação, sem incluir as ferramentas de compilação na imagem final.

