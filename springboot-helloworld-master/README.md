# Spring Boot Hello World

A spring boot enabled hello world application

- Executing as maven build with embedded tomcat application server
```
open maven sand box environmnet in Orelly, and follow below steps
git clone https://github.com/ngtrainings/HelloWorld/
cd /HelloWorld/springboot-helloworld-master
mvn clean package
java -jar target/helloworld-0.0.1-SNAPSHOT.jar
open WebPreview at portno: 8080
```

- To run this as a docker application (assumption docker is installed on your machine)
```
docker pull gazgeek/springboot-helloworld
docker container run -p 8080:8080 -d gazgeek/springboot-helloworld

Go to Browser and type http://localhost:8080/ or do curl http://localhost:8080/ on command prompt
```



