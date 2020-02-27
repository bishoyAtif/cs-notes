# Docker

## Why Docker

- Development and production environments are often configured differently, which makes it difficult to resolve problems quickly when something was broken. Docker solves this problem by allowing developers to package their applications in a portable way. Docker helps you create a reproducible environment.
- Different applications may need conflicting software requirements.

## Docker VS Hybervisors

- A hypervisor allows you to create a virtual machine(VM) into which you can install an operating system. You can install the necessary versions of software in them, and then you can run your application in it. In this way, all applications are isolated from one another.<br>
  ![Normal Virtualization Schema](https://i.ibb.co/7g4bBfc/Hypervisor1.png)
- Unfortunately, emulating hardware takes up significant resources, making this method slow, inefficient and power hungry. In addition, a separate OS is installed inside each VM, which adds to this overhead.
- A lightweight form of virtualization is called "operating system level virtualization", "containerization" or "layered file system" which enables the ```containers``` to share common parts and resources then the end result is that they are way less of resource-hog on the host system than a virtual machine.<br>
  ![OS Layered Virtualization](https://i.ibb.co/jwBb5W8/image.png)
- Docker creates stand-alone packages called ```containers``` that contain everything that is needed for you to run your application. Each container gets its own CPU, memory and network resources and does not depend on a specific operating system or kernel.

## How Docker Works

- We start out with a description file, called a ```Dockerfile```. In this ```Dockerfile```, we specify everything we need in terms of OS, environment variables and how to get our application in there.
- Typically, an ```image``` is created from a "Dockerfile", which contains the steps needed to create an ```image```. An "```image```" is a package that contains an application. Typically, an ```image``` includes executable files and shared libraries "all that’s needed for the application to run". This approach makes applications portable.
- You can think of a ```container``` as the runnable instance of an ```image```, with its own persistent file system and network access added to it. The ```container``` is completely isolated from the base system and the rest of the containers. You can make many container from the same image.
- After creating a container, you can "start" them. This executes the default command that’s been specified in the Dockerfile. However, you can also start up any other command. For example, you might want to inspect some files on an Ubuntu-based nginx container by running the bash shell in the image.
- To make things easier, you can also "run" images directly, and Docker will automatically create a container for you. You can also stop, re-run and delete containers as and when you need.
- Docker sets up networking between containers automatically. Specifically, it creates a network interface named docker0 on the host system, which allows it to create a virtual subnet from which IP addresses are allocated to individual containers. Many applications listen for inbound connections, and you can "expose" ports inside a container. You can also allow Docker to "publish" a port, which maps it to the host interface and makes it available to the outside world.

## General Commands

- ```docker version``` shows the current version for both docker server and client "Verifies that the client can talk to the server".
- ```docker info``` shows more info about config files, the client, the server, the images and containers you have.
- ```docker login``` login to your docker hub account to let your cli interact with it.
- ```docker logout``` logout from your docker hub account.
- ```docker system prune``` Remove all unused containers, networks, images and optionally volumes.
## Docker containers

## Dealing with Containers

- ```docker container run <image> <alternative command to run>``` run a new container from an image.
  - ```--publish or -p portFromLocal:portToContainer``` forwards a request to an extrnal local port to an internal port in the container. ```--publish 8000:80``` forwards the requests on the port 8000 for the host to the port 80 in the container.
  - ```-P``` publishes all the ports that are ```EXPOSE```d in the dockerfile of the image.
  - ```--detach or -d``` runs the container in the background.
  - ```--name <uniqueName>``` let you specify the name for the container.
  - ```--env or -e <key=value>``` let you specify environment variables when creating the container.
  - ```-it``` get a new virtual terminal for the new container and make its STDIN within the current shell.
  - ```-ia``` attaches the virtual terminal for the current container and make its STDIN within the current shell.
  - ```--rm``` automatically removes the container when it exits.
- ```docker container stop <id|nuiqueName>``` stop a running container.
- ```docker container start <id|nuiqueName>``` start a stopped container.
- ```docker container exec <flags> <id|nuiqueName> <command>``` executes an additional command on a running container, won't affect the main process it.
- ```docker container logs <id|nuiqueName>``` show the logs for a container.
- ```docker container top <id|nuiqueName>``` show the running processes for a container.
- ```docker container stats <id|nuiqueName>``` show live performance "memory and the cpu usage" for a container or more.
- ```docker container inspect <id|nuiqueName>``` show the meta data "volumes, network, configs" for a specific container.
- ```docker container rm <id|nuiqueName>``` remove a stopped container.
  - ```-f``` forces removal of a running container.
- ```docker container port <id|nuiqueName>``` shows published port from a specific container.
- ```docker container diff <containerName>``` show the changes files in the container with respect to the base image.
- ```docker container commit <containerName> <repoName/imageName:tag>``` commits the changes made within a container to a new image.
- ```docker container ps``` shows the running containers.
  - ```-a``` show all containers including the stopped ones.
- ```docker container commit <container> <tag>``` commits the changes made in a running container and saves them in a new base image with a specific tag.
  - ```-a <author>``` sets an author name for the commit.
  - ```-m <message>``` sets the commit message.

### Networking between containers

- Communication between containers should be done through the container name not ip "because ip can be changed as the container can be stopped or removed".
- This feature can be implemented by linking two containers together using ```--link <anotherContainer>``` flag when creating the container. But it's now **deprecated**.
- You can also implement this feature "DNS support and calling the containers by their name" by making a **new network** and connect all the containers to it so you can message other containers with their container name only like localhost.
- ```docker network ls``` shows available docker networks.
- ```docker network create <networkName>``` creates a new network.
- ```docker network inspect <network>``` shows info about a specific network "containers in this netowrk, ip adresses and more".
- ```docker network connecct <network> <container>``` add a container to a specific network.
- ```docker network disconnect <network> <container>``` remove a container from a specific network.
- ```docker container run --network <network>``` adds the container to a specific network.

## Docker Volumes
- Volumes or data volumes is a way for us to create a place in the host machine where we can write files so they are persisted. Typically we would want to store things like log files, JSON files and perhaps even databases (SQLite ) on a volume to be available even the container is removed or recreated.
- ```docker volume create <name of volume>``` this command creates a new volume.
- ```docker volume ls``` lists all the volumes on the local.
- ```docker volume prune``` removes all the volumes that aren't used be any containers.
- ```docker volume rm <name of volume>``` removes a specific volume.
- ```docker volume inspect <name of volume>``` gets info about this volume "the place to store data and more".
- ```docker container run -v <volumeName:/path/to/container/target/directory>``` creates or attaches a container to a local volume.
- ```docker container run -v </path/from/the/host:/path/to/container/target/directory>``` binds a directory from the local to a specific container directory "overwrite a directory in the container with a directory in the local". It simply mounts a host directory to a directory with the same name in the container.

## Docker Images

### Dealing With Images

- Docker images consists of a stack of layers. Each layer has a unique hash and it is shared between images to minimize the disk usage.
- The CoW "Copy On Write" is a strategy of sharing and copying files for maximum efficiency. If a file or directory exists in a lower layer within the image, and another layer (including the writable layer) needs read access to it, it just uses the existing file. The first time another layer needs to modify the file (when building the image or running the container), the file is copied into that layer and modified.
- Each Container is just a writable layer over the image.
- ```docker image ls``` shows all images cached in the local registery.
  - ```-q``` shows the ids of the cached images.
- ```docker image rm <imageId>``` removes an image from the cached registery by its id.
- ```docker image pull <imageName:version=latest>``` pulls the image requested from docker hub to the local registery.
- ```docker image history <imageName:version=latest>``` shows the layers of changes made on an image.
- ```docker image inspect <imageName:version=latest>``` shows the meta data and the default configs for a specific image.
- ```docker image tag <imageName:tag> <newImageName:newTag>``` adds a tag to a specific image.
- ```docker image push <imageName:tag>``` pushes a specific image with a tag to the logged-in docker hub account.

### Building Images

- ```docker image build <options> context```
  - ```context``` argument is a directory that acts as the base directory to make the commands from the ```Dockerfile``` within like ```COPY```.
  - ```-f or --file <filename = Dockerfile>``` specify a file to build. The default file is named ```Dockerfile``` in the current directory.
  - ```-t or --tag name:tag``` specify a name and a tag for the image.

#### Commands of ```Dockerfile```

- ```FROM <baseImage>``` specifies a base image to start with.
- ```ENV <key> <value>``` adds environment variables to the image.
- ```RUN <command>``` run bash commands within the image "usually used to install packages".
- ```EXPOSE <port> <anotherPort> ...``` documents the ports that should be exposed from the container to the outside world "You still need to use ```-p``` to expose them explicitly. ```EXPOSE don't actually open the ports".
- ```WORKDIR <directoryToChangeTo>``` changes the image's working directory to a specific directory.
- ```COPY <source> <destination>``` copies a file or directory from the local to the image.
- ```ADD <source> <destination>``` lets you do that too, but it also supports 2 other sources. First, you can use a URL instead of a local file or directory. Secondly, you can extract a tar file from the source directly into the destination .
- ```VOLUME <path>``` creates a data storage drive by specifying a local host path to save the data to.
- ```ENTRYPOINT ["list", "of", "command", "parts"]``` sets the command and parameters that will be **always** executed first when a container is run. Any command line arguments passed to ```docker run <image>``` will be appended to the entrypoint command.
- ```CMD [<command>]``` sets a default command to run when creating a container from this image. It will be overwritten when passing command argument to ``` docker run``` or ```docker exec``` containers.
  - ```CMD``` and ```ENTRYPOINT``` commands can be in two forms. Shell form ```echo "Hello world"```. it calls ```/bin/sh -c <command>``` under the hood and normal shell processing happens. And It can be in exec form ```["executable", "param1", "param2", ...]```. When instruction is executed in exec form it calls executable directly, and shell processing does not happen. It don't substitue variables or do any actions that related to bash. You should call bash explicitly if you need to use it ```["/bin/bash", "-c", "echo Hello, $name"]```.
  - Prefer ```ENTRYPOINT``` to ```CMD``` when building executable Docker image and you need a command always to be executed. Additionally use ```CMD``` if you need to provide extra default arguments that could be overwritten from command line when docker container runs.

## Docker Compose

- Docker Compose is a way to combine more than one container together. Usually you will need more than one container to provide a service, For example if you need to serve web app, you will need apache, mysql, cache and other components.
- You write the configuration for those combination in a YAML file with ```.yml``` extention. You will describe containers, networks, volumes in this file. Then use a cli tool called ```docker-compose``` to build this combination of containers from the yaml file.

### Dealing with Docker Compose

- ```docker-compose``` will build the yaml file in the current directory that is named ```docker-compose.yml``` file.
  - ```-f <fileName>``` run a custom named yaml file.
  - ```--build``` re-builds all the custom images specified in the yaml file.
- ```docker-compose up``` setup all the containers and create volumes and networks.
  - ```-d``` will run the composed containers in the background.
- ```docker-compose down``` stop all the containers and delete containers, volumes and networks.
  - ```--v``` removes volumes attached to the containers.
  - ```--rmi <type>``` remoevs built images. When using ```type=local``` removes only the custom built images.
- ```docker-compose exec <service> <command>``` executing command in a service within composed containers.
- ```docker-compose ps``` shows all the running containers.
- ```docker-compose top``` shows the processes running in the containers.

#### ```docker-compose.yml``` file

- You can use ```${variable}``` to assign dynamic values based on the host environment variables.