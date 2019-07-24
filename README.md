Docker Playgroud

BUILD/UPDATE Docker Image
docker build -t <image-name> .
docker run -d -p 80:80 <image-name>

PUSH DOCKER IMAGE IN hub.docker.com
Docker login. <- hubs.docker login credentials
Docker tag <image-name> nitrogen17/test_container
Docker push nitrogen17/test_container
