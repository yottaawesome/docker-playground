# Your first Docker container

https://www.katacoda.com/courses/docker/deploying-first-container

## Step 1 -- running a container

The objective of step is to run the `redis` container in the background.

We first need to locate the image on registry.hub.docker.com. The registry can be searched using the command: `docker search redis`.

To run the redis container in the background, we use `docker run -d redis`. The `-d` flag specifies the container should run in the bckground.

### Summary of commands

* `docker search <name>`
* `docker run <name>`

## Step 2 -- finding running containers

The command `docker ps` lists all running containers and basic information.

`docker ps <container-name|container-id>` displays additional details about the container.

`docker logs <container-name|container-id>` will display the logs the container has written to standard out.

### Summary of commands`

* `docker inspect <friendly-name|container-id>`
* `docker logs <friendly-name|container-id>`

## Step 3 -- accessing Redis

We now need to access the container. However, we cannot so far, because the container is sandboxed. To be able to access it, we need to map a port from the host to the container. We do so like follows.

`docker run -d --name redisHostPort -p 6379:6379 redis:latest`

This command assigns the container the name `redisHostPort` via the `--name` argument and maps port `6379` on the host to `6379` on the container.

### Summary of commands used

* `docker run -d --name <container-name> -p <host-port>:<container-port>`

Note: By default, the port on the host is mapped to `0.0.0.0`, which means all IP addresses. You can specify a particular IP address when you define the port mapping, for example, `-p 127.0.0.1:6379:6379`.

## Step 4 -- accessing Redis

Running on fixed ports is potentially problematic if we wish to run multiple `redis` instances. Thankfully, we can tell `docker` to expose `redis` on a randomly selected available port on the host.

`docker run -d --name redisDynamic -p 6379 redis:latest`

To discover which port has been assigned to the container, we can use `docker port redisDynamic 6379` or `docker ps`.

### Summary of commands used

* `docker run -d --name <container-name> -p <container-port> <image>`

## Step 5 -- persisting data

Containers are designed to be stateless. Binding directories (also known as volumes) is done using the option `-v <host-dir>:<container-dir>`. When a directory is mounted, the files which exist in that directory on the host can be accessed by the container and any data changed/written to the directory inside the container will be stored on the host. This allows you to upgrade or change containers without losing your data. Hence, we can use `docker run -d --name redisMapped -v /opt/docker/data/redis:/data redis` to tell the `redisContainer` to store the data on a directory shared with the host.

### Summary of commands used

* `docker run -d --name <container-name> -v <host-dir>:<container-dir> <image>`

## Step 6 -- running a container in ihe foreground

If we wanted to interact with the container (for example, to access a bash shell) she could include the options `-it`. In addition, certain images allow you to override the command used to launch the image. For example, the Ubuntu image can either run OS commands or run an interactive bash prompt using /bin/bash

The command `docker run ubuntu ps` launches an ubuntu container and runs `ps` on the container, while `docker run -it ubuntu bash` launches a Bash shell and connects to the container.

## Summary of commands used

* `docker run <image> <command>`
* `docker run -it <image> <command>`
