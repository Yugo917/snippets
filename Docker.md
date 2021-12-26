# Docker

```sh
-  $ docker -v # Get docker version
-  $ docker ps # Get container list
-  $ docker stop $(docker ps -a -q) # Stop all containers
-  $ docker rm $(docker ps -a -q) # Delete all containers
-  $ docker volume prune -f # Delete all volumes
-  $ docker rmi $(docker images -q) # Delete all images
-  $ docker build -t "MyImageName" . # Create your image
```

# DockerCompose

```sh
- $ docker-compose -v # Get docker-compose version
- $ docker-compose up # Up docker-compose.yml
- $ docker-compose -f myDockerComposeFile.yml up # Up specific docker-compose.yml 
- $ docker-compose -f myDockerComposeFile.yml up --build -d # Up and force rebuild
- $ docker-compose up NameOfMyService # Up specific service
- $ docker-compose rm -svf # Stop all container in the docker-compose.yml
```