# Steps to Demonstrate how to Deploy a Spring Boot App on AWS ECS Cluster
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

# clone project
git clone https://github.com/mydeveloperplanet/MyAWSPlanet.git
cd MyAWSPlanet

# build and create image
mvn clean verify
docker images

## Authenticate yourself to the AWS ECR public registry
aws configure

aws ecr-public get-login-password \
--region us-east-1 | docker login \
--username AWS --password-stdin public.ecr.aws

# my project
myimage="mydeveloperplanet/myawsplanet"


## Create a public repository in ECR
aws ecr-public create-repository \
--repository-name $myimage \
--region us-east-1

sudo yum install jq

## Get ECR repository url
URL=$(aws ecr-public describe-repositories \
--region us-east-1 | jq -r .repositories[].repositoryUri ) && echo $URL

## returns public.ecr.aws/z9l9d8r7/mydeveloperplanet/myawsplanet:latest

## TAG you docker image form ECR public repository
docker build -t $myimage .
docker tag $myimage:latest $URL

## PUSH a docker image from a private ECR repository
docker push $URL

# katacoda k8s url to validate the image
https://www.katacoda.com/courses/kubernetes/kubectl-run-containers
docker pull public.ecr.aws/z9l9d8r7/mydeveloperplanet/myawsplanet:latest

# without ALB
http://34.203.196.3:8080/
http://34.203.196.3:8080/name

http://MyAwsAlb-645179025.us-east-1.elb.amazonaws.com:8080/name

```
