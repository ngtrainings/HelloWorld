# Steps to Demonstrate Spring Boot on EKS — From Scratch to Hosting
```
# install AWS CLI
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo yum install unzip
sudo unzip awscliv2.zip
sudo ./aws/install
aws --version

#install maven
sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
sudo yum install -y apache-maven
mvn –version

# install docker
sudo rm /etc/yum.repos.d/docker-ce.repo # if you have already tried in the wrong way
sudo amazon-linux-extras install docker

# enable on boot and start daemon
sudo systemctl enable docker
sudo systemctl start docker

# correct permissions
sudo usermod -a -G docker $USER
newgrp docker
docker ps

#Perform a quick update on your instance:
sudo yum update -y
 
#Install git in your EC2 instance
sudo yum install git -y
 
#Check git version
git version

#install minicube
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
&& chmod +x minikube \
&& sudo mv minikube /usr/local/bin/
minikube start

# install java
sudo apt-get install openjdk-11-jdk

###############################################

# katacoda url
https://www.katacoda.com/courses/kubernetes/kubectl-run-containers

# clone project
git clone https://github.com/kvr2277/spring-boot-eks
cd spring-boot-eks
sed -i 's/Vinod/AWengerS/g' src/main/java/com/example/demo/HelloController.java

# test package locally
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
mvn install
java -jar target/*.jar &
curl localhost:8080/name

# build package
mvn spring-boot:build-image

# configure local registery
docker run -d -p 5000:5000 --restart=always --name registry registry:2

#tag the image
docker tag eksdemo:0.0.1-SNAPSHOT localhost:5000/eksdemo

#push image to docker push localhost repo
docker push localhost:5000/eksdemo

# deploy local image
#update testdemo to eksdemo in deployment.yaml file
sed -i 's/testdemo/eksdemo/g' deployment.yaml
kubectl apply -f deployment.yaml
kubectl get all
kubectl port-forward svc/demo 8083:8080 &
curl localhost:8083/name


## Authenticate yourself to the AWS ECR public registry
aws configure

aws ecr-public get-login-password \
--region us-east-1 | docker login \
--username AWS --password-stdin public.ecr.aws

# my project
myimage="demo-repo"

## Create a public repository in ECR
aws ecr-public create-repository \
--repository-name $myimage \
--region us-east-1

sudo yum install jq

## Get ECR repository url
URL=$(aws ecr-public describe-repositories \
--region us-east-1 | jq -r .repositories[].repositoryUri ) && echo $URL

## TAG you docker image form ECR public repository
docker tag eksdemo:0.0.1-SNAPSHOT $URL

## PUSH a docker image from a private ECR repository
#public.ecr.aws/z9l9d8r7/demo-repo:latest
docker push $URL

![repo](https://user-images.githubusercontent.com/89327844/170221041-0a64bae4-a912-47a4-ab18-1ef58cba5725.png)


## Install eksctl 
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version


# update cluster.yaml with subnet id and deploy
eksctl create cluster -f cluster.yaml
kubectl get svc
kubectl get pods --all-namespaces -o wide

# deploy the images
kubectl apply -f eks-deployment.yaml
kubectl get deployments

# deploy the service
kubectl apply -f eks-service.yaml



```
