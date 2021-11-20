[<- Home](README.md)
# Docker
## Transport d'images
Save image to archive : `docker save myimage:latest | gzip > myImage.tar.gz`  
Load image from archive : `docker load < myImage.tar.gz`
Save and load via ssh : `docker save myimage:latest | ssh user@adress "docker load"`

## Cleaning
Delete dangling Docker images : `docker rmi $(docker images -q -f dangling=true)`  
Kill all runnning docker containers : `docker kill $(docker ps -q)`  
Remove all stopped containers : `docker rm $(docker ps -a -q)`  
Remove all containers with image name :   
`docker rm $(docker stop $(docker ps -a -q --filter ancestor=imageName --format="{{.ID}}"))`  

## Resource usage
Get docker container including size : `docker ps -s`  
Get container disk utilization : `docker system df`

## More
Bash shell into container : `docker exec -i -t /bin/bash` (if bash is not available use /bin/sh)  