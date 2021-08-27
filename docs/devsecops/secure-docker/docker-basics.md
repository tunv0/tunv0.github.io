# Docker Basics

## Docker commands

[https://docs.docker.com/engine/reference/commandline](https://docs.docker.com/engine/reference/commandline)

### Images

Pull image

``` bash
docker pull ubuntu
```

Run image:

``` bash
docker run -i -d --name myubuntu ubuntu
```

* `-d` for running in the backgound
* `–interactive` or `-i` argument keep the container running

Check history in images

``` bash
docker image history image-name
```

### Containers

Run a command in a running container

``` bash
docker exec myubuntu whoami
```

spawn a shell in the container

``` bash
docker exec -it myubuntu bash
```

List containers

``` bash
docker ps -a
```

Show the running processes of a container

``` bash
docker top myubuntu
```

Check logs in the container

``` bash
docker logs CONTAINER_ID
```

## Manage Data In Docker

### Docker volumes

create volume

``` bash
docker volume create data
```

``` bash
/# ls /var/lib/docker/volumes/
data  metadata.db
```

run a container to use data volumes

``` bash
docker run --name ubuntu -d -v data:/opt -it ubuntu:18.04
```

### Bind mounts

``` bash
docker run --name ubuntu -d -v /opt:/opt -it ubuntu:18.04
```

### tmpfs mounts

[https://docs.docker.com/storage/tmpfs/](https://docs.docker.com/storage/tmpfs/)

## Docker Registry

### Deploy local registry

[https://docs.docker.com/registry/deploying/](https://docs.docker.com/registry/deploying/)

``` bash
docker run -d -p 5000:5000 --restart=always --name registry registry:2
```

### Store the images

add the image name with the registry url as a prefix

``` bash
docker tag ubuntu:1.0 localhost:5000/ubuntu:1.0
```

push the image to the docker registry

``` bash
docker push localhost:5000/ubuntu:1.0
```

check images on the registy

``` bash
curl localhost:5000/v2/_catalog
```

## Docker Networking

### Basic commands

See available networks

``` bash
docker network ls
```

``` bash
docker network list
```

remove

``` bash
docker network rm mynetwork
```

|Network	|Descriptions|
|--|--|
|bridge|	This is the default network driver when you don’t specify a driver to the containers. Containers on the same bridged network can speak to each other, but are isolated from containers on other bridged networks. All containers can access the external network through NAT|
|host|	The containers use the host’s networking directly, while retaining separation on storage and processing. Ports exposed by the container are exposed on the external network using the host’s IP address|
|macvlan|	When creating a macvlan, you assign a parent network device (e.g. “eth0”). Each container on the macvlan network will receive its own MAC address on the network that eth0 is connected to. Each container has full network access. Warning: when misconfigured, you may overrun the network with too many MACs, or you may duplicate IP addresses|
|none|	networking is disabled with this network driver, containers cannot communicate to each others, nor with the external network|

### Bridge config

[https://blog.oddbit.com/post/2018-03-12-using-docker-macvlan-networks/](https://blog.oddbit.com/post/2018-03-12-using-docker-macvlan-networks/)

Create new and view detail

``` bash
docker network create mynetwork
```

``` bash
docker network create --subnet 192.10.1.0/16 app
```

``` bash
docker inspect mynetwork
```

attach container using `mynetwork`

``` bash
docker run -d --name ubuntu --network mynetwork -it ubuntu:18.04
```

connect to running container

``` bash
docker network connect app ubuntu
```

### macvlan config

create

``` bash
docker network create --driver macvlan mymacvlan
```

attach container using `mymacvlan`

``` bash
docker run -d --name ubuntu --network mymacvlan -it ubuntu:18.04
```

detail vlan for container

``` bash
docker inspect ubuntu -f "{{json .NetworkSettings.Networks }}" | jq
```

[https://docs.docker.com/network/macvlan/](https://docs.docker.com/network/macvlan/)

### none config

create

``` bash
docker run -d --name ubuntu --network=none -it ubuntu:18.04
```

## Create Docker Image

### Dockerfile

=== "Dockerfile"

	``` bash
	# FROM python base image
	FROM ubuntu:18.04

	# COPY startup script
	COPY . /app

	WORKDIR /app

	RUN apt update && apt install nginx -y
	RUN apk add --no-cache gawk sed bash grep bc coreutils

	# EXPOSE port 8080 for communication to/from server
	EXPOSE 8080

	ENTRYPOINT ["/bin/bash", "-c"]
	# CMD specifcies the command to execute container starts running.
	CMD ["/app/run_app_docker.sh"]
	```

=== "Syntax Description"

	|Syntax|Description|
	|--|--|
	|FROM:| Creates a layer from Docker Image. Specifies the base image to use.|
	|COPY:| Copies the files from the local directory to the docker image on a specific location.|
	|ADD:| Similar to COPY but supports file download (HTTP), auto extracting compressed file(s), and replacing the existing file to a specific location if needed forcefully.|
	|RUN:| Run OS command (just like you would do on a terminal) but only executes it during the image creation process.|
	|ENTRYPOINT:| Run a command as the default command when the container starts. Its the entrypoint to the utility/command.|
	|CMD:| Command to run when a container starts or arguments to ENTRYPOINT if specified.|

[https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/](https://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/)

`sleep infinity` tells the container to keep the process alive.

``` bash
FROM ubuntu:18.04

RUN apt update && apt install nginx -y

CMD ["/bin/bash", "-c" , "service nginx start; sleep infinity"]
```

### Build Image

[https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/)

``` bash
docker build -f /path/to/a/Dockerfile -t shykes/myapp .
```

* `-f` flag with docker build to point to a Dockerfile anywhere in your file system
* `-t` tag at which to save the new image

## Docker Compose

### Introduction

Dockerfile: handle 1 container

Docker Compose: handle multiple containers using a single file called docker-compose.yml

``` bash
version: "3"
 
services:
  ubuntu:
    image: ubuntu:18.04
    stdin_open: true        # the same way like docker run -i
```

Run

``` bash
docker-compose up -d
```

### Compose file

=== "docker-compose.yml"

	``` bash
	version: "3"

	services:
	  web:
	    image: nginx
	    container_name: webserver       # name of container
	    ports:
	     - "80:80"                      # similar to docker run -p 80:80
	    environment:
	     - NGINX_HOST=example.com       # similar to docker run -e VAR=value
	    volumes:
	     - ./:/var/www/html/app             # ./ means a bind mounts
	     - image_data:/var/www/html/images  # image_data means use docker volume

	volumes:
	  image_data:                       # similar to docker volume create
	```

=== "Syntax Descriptions"

	|Syntax|	Descriptions|
	|--|--|
	|version|	Version of compose file format to use, check out this link|
	|image|	Specify the image to run|
	|container_name|	Specify a custom container name, rather than a default name|
	|ports|	Expose port(s), similar to docker run -p argument|
	|environment|	Add environment variables into the container by defining a key-value pair|
	|volumes|	Volumes to save our data persistently using various options type like bind or volumes|