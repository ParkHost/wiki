---
title: Docker
description: 
published: true
date: 2021-03-27T17:27:11.721Z
tags: docker
editor: markdown
dateCreated: 2020-06-17T14:04:28.702Z
---

![docker[1].png](/docker[1].png =150x125){.align-left}
is a PaaS that uses OS-level virtualization to deliver software in packages called containers.
Containers are isolated from one another and bundle their own software, libraries and configuration files;
they can communicate with each other through well-defined channels

---

# Overview
It uses Yaml as config file to set everything before creating your container.
 
All of my project (including wikijs) is running within a docker container.
Docker is native quicker and after some research probably easier then LXC.

> VSCode: Docker Extension (ms-azuretools.vscode-docker)
{.is-warning}


# Dockerfile
**Dockerfile lets you create your own (golden) image from a baseImage from Docker-Hub**

Create a Dockerfile (called Dockerfile)
![dockerfile.png](/dockerfile.png)


```docker
# Example Script:
FROM baseImage # (dockerhub) e.g. node:latest

COPY . . # (source destination)

RUN npm install
# can use multi RUN commands

CMD [ "node", 'src/index.js' ] # array of commands
CMD node src/index.js #(same result as the sentence above)

```
---

# Docker-compose
**is a yml file with a pre-defined container configuration**

```yml
# Example file
# set the docker-compose version
version: { version number as string }

# Setup the services you wanna run and define the container(s)
services:
  { serviceName }:
    container_name: { containerName }
    image: { imageName (e.g from docker-hub of own created with a Dockerfile) }
    volumes:
     - { Optional: specify the volume you wanna redirect into the container }
    restart: { reboot options } 
    expose:
     - { Optional: portnumber as string you wanna expose to other containers }
    command: { optional: command will run every time your spin up the container through docker-compose }
        
```
# Dockerfile in combination with docker-compose
Found this solution on Stack
[Source](https://stackoverflow.com/a/47907859/8716338)


first the `docker-compose.yml` (watch the build proces)
```yml
version: '3'
	services:
  	example_service:
    	build:
      	context: ./image
      	dockerfile: Dockerfile
    	container_name: example_docker
    	stdin_open: true
```
now the `Dockerfile`:

```yml
FROM alpine:latest

RUN apk update && apk upgrade && \
    apk add git
``` 

> make sure you dont have the data in the image folder, otherwise it will a be redirected into the new image
{.is-info}



# Commands

Some starting commands to get your docker up and runnin'

## building your image:
```bash
docker build -t name(or CompanyName)/Imagename:tag(or version) . (where to find the Dockerfile)
```
---

## Shows every (docker)image installed
```bash
docker image ls
```
---

## Spin up the docker container with specifying the ports and the builded image
```bash
docker run -p portOutside(on your sysem):portInside(code) imagename
```
---

## Shows the currently running containers:
```bash
docker container ls
```
---

## Stopping your container
```bash
docker stop {containerName}
```
---
## Start a shell inside container

```docker
docker exec -it {containerName} /bin/bash
```
---
## Show build logs

```docker
docker logs -f {containerName}
```
---
## Remove container

```docker
docker rm {containerName}
```
---
## Show docker volumes

```docker
docker volume ls
```
---
## .....

```docker
Docker Command
```
# Tips

## Reverse proxy - Route external traffic to container
If containers are connected to the same docker network, they can communicate through hostname. I made a NGinX container which routes the external public traffic to the requested container. **Without** the use of the 'jwilder docker image'. This construction creates a `zone` which will never expose ports of the HOST itself. 


## Attach volumes to your docker container
> Docker has a volume feature. Volumes can be connected to your container. 
> Volumes are `'mounted'` drives and contains the data you pointing to in the `docker-compose.yml` file or dynamically created.
> The command: `docker volume ls` shows all created volumes
> {.is-success}

```yml
version: '3'

services:
  name:
    container_name: container01
    image: nginx:1-alpine
    volumes:
      - /folder/host/location:/folder/container/location
    restart: unless-stopped

```

## Create your own image with docker.
First containerize a baseImage and edit as you wish.
Use the following command to `capture` the container back into a image:

```bash
docker commit -m="Alpine Nginx with Nodejs" -a "Parkhost" yourBaseImageContainerName New/imageName:version
```

 - `-m` option to provide a message describing the changes.
 - `-a` option to provide author information.

## Automatic update Docker images
[Watchtower](https://github.com/containrrr/watchtower) updates your Docker images automatically.
By default it will update all containers if you haven't specified an image version in your container config.

docker-compose file:
```docker
version: '3'

services:
  watchtower:
    container_name: watchtower
    image: containrrr/watchtower
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /root/.docker/config.json:/config.json
    restart: unless-stopped
    environment:
#     -  WATCHTOWER_SCHEDULE: 0 0 21 * * ?
      - WATCHTOWER_POLL_INTERVAL=7200
      - WATCHTOWER_CLEANUP=true
#      - WATCHTOWER_DEBUG=true
      - TZ=CET



```
> 
> [By default it will check every 5 minutes, Docker-Hub has a rate limiting of 100 pulls per 6 Hours (free tier), schedule your watchtower wisely!](https://www.docker.com/increase-rate-limits?utm_source=docker&utm_medium=web%20referral&utm_campaign=increase%20rate%20limit&utm_budget=)
{.is-danger}

