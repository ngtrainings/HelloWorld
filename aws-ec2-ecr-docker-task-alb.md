# Steps to Demonstrate how to Deploy a Spring Boot App on AWS ECS Cluster
- Steps to Demonstrate how to Deploy a Spring Boot App on AWS ECS Cluster
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

# clone project
git clone https://github.com/mydeveloperplanet/MyAWSPlanet.git

# build and create image
mvn clean verify
docker images

#public ECR
public.ecr.aws/z9l9d8r7/mydeveloperplanet/myawsplanet:latest

# push image to ECR
aws configure
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/z9l9d8r7
docker build -t mydeveloperplanet/myawsplanet .
docker tag mydeveloperplanet/myawsplanet:latest public.ecr.aws/z9l9d8r7/mydeveloperplanet/myawsplanet:latest
docker push public.ecr.aws/z9l9d8r7/mydeveloperplanet/myawsplanet:latest


```