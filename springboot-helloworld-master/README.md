# Spring Boot Hello World

A spring boot enabled hello world application

- Executing as maven build with embedded tomcat application server


mvn clean package
java -jar target/helloworld-0.0.1-SNAPSHOT.jar


- To run this as a docker application (assumption docker is installed on your machine)
```
docker pull gazgeek/springboot-helloworld
docker container run -p 8080:8080 -d gazgeek/springboot-helloworld

Go to Browser and type http://localhost:8080/ or do curl http://localhost:8080/ on command prompt
```



