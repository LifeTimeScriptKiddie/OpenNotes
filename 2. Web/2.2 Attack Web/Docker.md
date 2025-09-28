---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/docker/","noteIcon":"","created":"2025-04-15T14:11:19.602-04:00"}
---


















## Basic Commands
```zsh
docker version #Get version of docker client, API, engine, containerd, runc, docker-init
docker info #Get more infomarion about docker settings
docker pull registry:5000/alpine #Download the image
docker inspect <containerid> #Get info of the contaienr
docker network ls #List network info
docker exec -it <containerid> /bin/sh #Get shell inside a container
docker commit <cotainerid> registry:5000/name-container #Update container
docker export -o alpine.tar <containerid> #Export container as tar file
docker save -o ubuntu.tar <image> #Export an image
docker ps -a #List running and stopped containers
docker stop <containedID> #Stop running container
docker rm <containerID> #Remove container ID
docker image ls #List images
docker rmi <imgeID> #Remove image
docker system prune -a
#This will remove:
#  - all stopped containers
#  - all networks not used by at least one container
#  - all images without at least one container associated to them
#  - all build cache


docker-compose down #Stop existing instance.
docker-compose up  # start a new, independent container
docker-compose exec  # Run inside existing running service container. 
docker logs -n 5 <container name>
```



These files indicates the use of Docker Containers
```
docket-compose.yml
Dockerfile
```


## Docker Files structure
https://dev.to/devlcodes/file-structure-of-a-node-project-3opk


## Docker Architecture


![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Images/Pasted%20image%2020240618154005.png)
https://www.geeksforgeeks.org/architecture-of-docker/



![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Images/Pasted%20image%2020240618154039.png)



https://docs.docker.com/guides/docker-overview/



![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Images/Pasted%20image%2020240618154118.png)

Docker Architecture is the backbone of this powerful platform.

It follows a client-server model, and includes major components such as the Docker Client, Docker Host, Docker Images, Docker Containers, and Docker Registry.

Let’s take a closer look:

Docker Client: The starting point of our Docker journey! 🚀

The Docker client provides a way for users to interact with Docker.

When we fire a Docker command, the Docker client sends these instructions to the Docker daemon, which carries out the requested tasks.

Docker Daemon: Taskmaster on the scene! 👷‍♂️

The Docker daemon runs on the host machine and handles all requests from the Docker client, such as building, running, and distributing Docker containers.

Docker Images: Your application’s blueprint. 🏢

Docker Images are read-only templates that form the basis of containers.

They include all the dependencies your application needs to run effectively.

Docker Containers: Running instances of Docker images. 🏃‍♂️

A Docker container holds everything needed to run an application — the code, runtime, libraries, environment variables, and configuration files.

Docker Registry: Like a library for Docker Images! 📚

The Docker registry is where Docker images live.

Docker Hub is a public registry that anyone can use, but you also have the option of creating your own private registry.

The four most basic Docker commands are illustrated in the attached image -

Docker Pull

𝚍𝚘𝚌𝚔𝚎𝚛 𝚙𝚞𝚕𝚕 𝚙𝚘𝚜𝚝𝚐𝚛𝚎𝚜
• Checks if the image is already downloaded locally.
• If not, it will download the image from Docker Hub.
• Docker Hub is a public registry where Docker images are stored.

Docker Build

𝚍𝚘𝚌𝚔𝚎𝚛 𝚋𝚞𝚒𝚕𝚍 .
• Builds the current Dockerfile and creates a local image for your application.
• The Dockerfile is a text file that contains the instructions for building the image.
• Can be used to build custom images for your applications.

Docker Push

𝚍𝚘𝚌𝚔𝚎𝚛 𝚙𝚞𝚜𝚑 <𝚊𝚙𝚙𝚕𝚒𝚌𝚊𝚝𝚒𝚘𝚗 𝚒𝚖𝚊𝚐𝚎>
• Uploads the image/extension/plugin to Docker Hub.
• Can be used to share your images with others.

Docker Run

• Takes an image and runs a container from it.
• The container will run the image’s executable and expose the image’s ports.
• Can be used to start a web server, a database, or any other type of application.
𝚍𝚘𝚌𝚔𝚎𝚛 𝚛𝚞𝚗 𝚗𝚐𝚒𝚗𝚡




https://medium.com/@saddy.devs/understanding-docker-architecture-934ecd042b5f




![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Images/Pasted%20image%2020240618154154.png)


https://medium.com/@basecs101/understanding-docker-architecture-latest-c7a165571d89



![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Images/Pasted%20image%2020240618154228.png)

https://www.cherryservers.com/blog/a-complete-overview-of-docker-architecture




https://book.hacktricks.xyz/network-services-pentesting/2375-pentesting-docker



https://book.hacktricks.xyz/linux-hardening/privilege-escalation/docker-security

docker basic format
https://github.com/matomo-org/docker/blob/master/.examples/apache/docker-compose.yml

## Docker debugging ports
```
Port 9229:9229
Port 9228:9228

```


https://dejandayoff.com/the-danger-of-exposing-docker.sock/


