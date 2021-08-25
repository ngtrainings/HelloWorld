# HelloWorld
# Spring Boot Hello World

A spring boot enabled hello world application

## Usage

- Directly using maven
```
mvn spring-boot:run
```

- From within your IDE right click run 
```
Application.java
```

- From executable jar file
```
mvn clean install
java -jar target/helloworld-0.0.1-SNAPSHOT.jar
```

- To run this as a docker application (assumption docker is installed on your machine)
```
git clone https://github.com/ngtrainings/HelloWorld.git
docker run -p 80:2020 -d springboot-helloworld

Go to Browser and type http://localhost:8080/ or do curl http://localhost:8080/ on command prompt
```
