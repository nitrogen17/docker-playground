## Docker Playgroud

```
BUILD/UPDATE Docker Image
docker build -t <image-name> .
docker run -d -p 80:80 <image-name>

PUSH DOCKER IMAGE IN hub.docker.com
Docker login. <- hubs.docker login credentials
Docker tag <image-name> nitrogen17/test_container
Docker push nitrogen17/test_container

CHECK Docker image size via remote
* docker image inspect komljen/drone-kubectl-helm:latest --format='{{.Size}}'
Or pull docker image and execute this command
Docker images - in the last column


========= DOCKER ========

#stop all containers: docker stop $(docker ps -a -q)
#stop all containers by force docker kill $(docker ps -q)
#remove all containers docker rm $(docker ps -a -q)
#remove all docker images docker rmi $(docker images -q)
#purge the rest docker system prune --all --force --volumes

========================

Step 1:
$ mkdir myapp (create our app folder)
$ cd myapp (lets go into our folder)
$ nano Dockerfile (create a file called Dockerfile)

nano Dockerfile 
=====================================
FROM ubuntu:18.04
MAINTAINER Nitrogen <nitrogen17@google.com>
RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
ENV APACHE_RUN_USER  www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR   /var/log/apache2
ENV APACHE_PID_FILE  /var/run/apache2/apache2.pid
ENV APACHE_RUN_DIR   /var/run/apache2
ENV APACHE_LOCK_DIR  /var/lock/apache2
ENV APACHE_LOG_DIR   /var/log/apache2
RUN mkdir -p $APACHE_RUN_DIR
RUN mkdir -p $APACHE_LOCK_DIR
RUN mkdir -p $APACHE_LOG_DIR
COPY index.html /var/www/html
EXPOSE 80
CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]
=====================================

$ nano index.html

nano index.html
=====================================
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>First APP</title>
</head>
<body>
    <h1>People becoming Humans Again</h1>
</body>
</html>
=====================================

Step 2:
# Build an image using the Dockerfile at current location
# Example: docker build -t [name] .
$ docker build -t clever .

Note: Docker must already installed in PC

Step 3:
$ docker run -d -p 80:80 clever

DONE!


How do I SSH into a running container
There is a docker exec command that can be used to connect to a container that is already running.
* Use docker ps to get the name of the existing container
* Use the command docker exec -it <container name> /bin/bash to get a bash shell in the container
* Generically, use docker exec -it <container name> <command> to execute whatever command you specify in the container.
http://phase2.github.io/devtools/common-tasks/ssh-into-a-container/


Running Nano in Docker Image Container

docker exec -it id_container bash
apt-get update
apt-get install nano
export TERM=xterm


https://stackoverflow.com/questions/27826241/running-nano-in-docker-container/27827924


================ ADD Docker as sudoer ================ 
To create the docker group and add your user:
1. Create the docker group. $ sudo groupadd docker
2. Add your user to the docker group. $ sudo usermod -aG docker $USER
3. Log out and log back in so that your group membership is re-evaluated. 
================================================== 



```

References:

https://medium.com/faun/how-to-build-a-docker-container-from-scratch-docker-basics-a-must-know-395cba82897b

