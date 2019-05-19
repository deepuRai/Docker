#Dockerize PHP Application on Ubuntu 18.04

Step 1 :- Install docker with below url 

https://linuxconfig.org/how-to-install-docker-on-ubuntu-18-04-bionic-beaver


Step 2 :- Install Git by running "sudo apt-get install  git"

Step 3:- Clone Git Repository

mkdir docker_php
cd docker_php
git clone https://github.com/deepuRai/Docker.git


Step 4 :- Create a file with name “Dockerfile” inside docker_php directory. Copy below contents to the Dockerfile and save it.

FROM ubuntu:18.04
MAINTAINER Deepak Rai <deepak.ray1987@gmail.com>
 
#Update Repository
RUN apt-get update -y
 
#Install Apache
RUN apt-get install -y apache2
 
#Install PHP Modules
RUN apt-get install -y php7.0 libapache2-mod-php7.0 php7.0-cli php7.0-common php7.0-mbstring php7.0-gd php7.0-intl php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-zip
 
#Copy Application Files
RUN rm -rf /var/www/html/*
ADD dockerize-php-application /var/www/html
 
#Configure Apache (Optional)
RUN chown -R www-data:www-data /var/www
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
 
#Open port 80
EXPOSE 80
 
#Start Apache service
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]



Step 5 :- Build new Docker image using below command

docker build -t drai/dockerize-php-application .


Step 6 :- Display docker images

docker images


Step 7 :- Start a Docker container based on the new image

docker run -itd -p 80:80 drai/dockerize-php-application

Step 8 :- Check container status using below command and make sure the status is UP

docker ps -a


Step 9 :- Access the application using below URL

http://host/index.php


#Pushing image to docker hub 


Step 1 :- Login to shell of Docker container using below command

	docker exec -it  bash

Step 2 :- Use below command to login to Docker Hub. Provide your Docker Hub username and password when prompted

	docker login

Step 3 :- Push your image to Docker Hub using below command

	docker push drai/dockerize-php-application



Other Info about Docker 

Pull Docker image from Docker Hub

	docker pull drai/dockerize-php-application

Remove Docker image

	docker rmi -f 

Remove docker container

	docker rm -f 
	docker rm -f $(docker ps -aq)

