
exemplo de deploy do meu app todolist em spring

```dockerfile
FROM ubuntu:20.04 AS build

  

RUN apt-get update

RUN apt-get install openjdk-17-jdk -y

  

COPY . .

  

RUN apt-get install maven -y

RUN mvn clean install

  

FROM openjdk:17-jdk-slim

  

EXPOSE 8080

  

COPY --from=build /target/todolist-1.0.0.jar app.jar

  

ENTRYPOINT [ "java", "-jar", "app.jar" ]
```

pelo site dashboard render, criei um webservice

algumas considerações. Ele está buscando o  /target/todolist-1.0.0.jar

ele se baseia no artifactId e na version para criar o jar. Alterei para 

```xml
<groupId>br.com.jonascamargo</groupId>

<artifactId>todolist</artifactId>

<version>1.0.0</version>

<name>todolist</name>
```

para ele buscar esse arquivo descrito. Por fim, preciso fazer o commit

```git
git add .
git commit -m "nome do commit"
git push
```