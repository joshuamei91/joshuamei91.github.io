---
layout: page
title: Docker Cheatsheet
permalink: /docker-cheatcheet/
---

## Common workflows
- Run with specific env file and mount volume

```
docker run -d \
  --name mycontainer
  --env-file <path to env file> \
  -p hostport:containerport \
  --mount type=bind,source=<absolute path to source dir>,target=/path/in/container \
  --network <network name> \
  --restart=unless-stopped 
  xyz/myimage:tag
```

- Execute an interactive bash shell on the container

```
docker exec -it <container> bash
```

## Images

### Listing images
- List the most recently created images: `docker images`
- Show only image IDs: `docker images -q`
- List images by name and tag: `docker images [REPOSITORY[:TAG]]`
- Show untagged images: `docker images --filter "dangling=true"`

### Pulling images
- Pull an image or a repository from a registry: `docker pull`
- Pull from a different registry: `docker pull myregistry.local:5000/testing/test-image`

### Save and load images
- Save one or more images to a tar archive: `docker save xyz/myimage:tag > somename.tar`
- Load an image from a tar archive: `docker load -i somename.tar`

### Removing images
- Remove one or more images: `docker image rm [OPTIONS] IMAGE [IMAGE...]`
- Remove all dangling images. If -a is specified, will also remove all images not referenced by any container: `docker image prune`
- Remove all untagged images (dangling): `docker rmi $(docker images -f "dangling=true" -q)`

### Managing images
- Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE: `docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`

## Build 
*use .dockerignore to exclude files from the context*
- Build with PATH: `docker build .`
- Build with URL: `docker build https://github.com/docker/rootfs.git#container:docker`
- Build and tag the image: `docker build -t REPOSITORY:TAG .`
- Specify a Dockerfile: `docker build -f Dockerfile.debug .`
- Add entries to container hosts file: `docker build --add-host=docker:10.180.0.1 .`

## Containers
### Listing containers
- List running containers: `docker ps`
- List running and stopped containers: `docker ps -a`
- Filter by network: `docker ps --filter network=net1`

### Running containers
- Start container: `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`
  
  ***OPTIONS***
  - `-d`: Run container in background
  - `-e`: Set environment variables
  - `--entrypoint`: Overwrite the default ENTRYPOINT of the image
  - `--env-file`: Read in a file of environment variables
  - `--expose`: Expose a port or a range of ports on the container
  - `--hostname`: Container host name
  - `--ip`: IPv4 address
  - `-l`: Set meta data on a container (label)
  - `-m`: Memory limit
  - `--mount`: Attach a filesystem mount to the container
  - `--name`: Assign a name to the container
  - `--net`: Connect a container to a network
  - `-p`: Publish a container's port(s) to the host
  - `--restart`: Restart policy to apply when a container exits. Default: no
  - `--rm`: Automatically remove the container when it exits
  - `-v`: Bind mount a volume
  - `-w`: Working directory inside the container

- Stop container: `docker stop <container id>`
- Stop all containers: `docker stop $(docker ps -aq)`
- Remove container: `docker rm <container id>`
- Remove all containers: `docker rm $(docker ps -aq)`

### Running commands in the container
Run a command in a running container: `docker exec [OPTIONS] <container> <command>`


## Utilities
- Copy files/folders between a container and the local filesystem: `docker cp CONTAINER:SRC_PATH DEST_PATH`

## Networking
- Get an instance’s IP address: `docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' $INSTANCE_ID`
- List all port bindings: `docker inspect --format='{{range $p, $conf := .NetworkSettings.Ports}} {{$p}} -> {{(index $conf 0).HostPort}} {{end}}' $INSTANCE_ID`
- Find IP of docker0 bridge: `docker network inspect bridge` 
- Create network: `docker network create <network name>`

## Dockerfile

## Docker compose