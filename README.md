# Spring Boot Hello World

A spring boot enabled hello world application

- Executing as maven build with embedded tomcat application server
```
open maven sand box environmnet in Orelly, and follow below steps
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master
mvn clean package
java -jar target/helloworld-0.0.1-SNAPSHOT.jar
open WebPreview at portno: 8080
```

- To run this as a docker application (assumption docker is installed on your machine)
```
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master/
docker build -t helloworld .
docker images
docker run -p80:2020 helloworld
open WebPreview at portno: 80
```

- To run this as a docker application with oracle jdk 
```
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master/
create Dockerfile with below content

FROM store/oracle/serverjre:1.8.0_241-b07
COPY . /data/springboot-helloworld
WORKDIR /data/springboot-helloworld
EXPOSE 2020
CMD ["java", "-jar", "helloworld-0.0.1-SNAPSHOT.jar"]

login with docker id
docker build -t helloworld .
docker images
docker run -p80:2020 helloworld
open WebPreview at portno: 80
```

