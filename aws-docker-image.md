# Spring Boot Hello World
- Steps to prepare docker image from github and push to dockerhub repo
```
maven sandbox - orielly - https://learning.oreilly.com/scenarios/maven-compiling-packaging/9781492088677/
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master
mvn clean package
push jar to github repository

docker sandbox - orielly  - https://learning.oreilly.com/scenarios/docker-sandbox/9781492086161/
git clone https://github.com/ngtrainings/HelloWorld/
cd HelloWorld/springboot-helloworld-master
docker build -f Dockerfile-Spring -t ngtrainings/springboot-helloworld-master:v7 .
docker images
docker login
docker push ngtrainings/springboot-helloworld-master:v7

Custom image 	- ngtrainings/springboot-helloworld-master:v7

github link 	- https://github.com/ngtrainings/HelloWorld/tree/main/springboot-helloworld-master

dockerhub link 	- https://hub.docker.com/repository/docker/ngtrainings/springboot-helloworld-master

```