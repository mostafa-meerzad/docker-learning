# Docker

## What is Docker

Docker is a platform for building, running and shipping applications. It aims to solve the "it works on my machine"
problem by packaging your application with all it's dependencies, environment variables and specific dependency versions in a stand along containers that can run on any environment (development, production or testing).

## Containers vs Virtual Machines

Virtual Machines are resource intensive, slow to start and can introduce more complexity when you have to run multiple apps and different version.

Containers share the same resource with the host OS, they are fast to start and you can run different versions of the same app without interfering with one another.

**Container**: Is an isolated environment for running an application.

**VM**: Is an abstraction of a machine (physical hardware).

## Docker Architecture

Docker uses a **Client/Server** architecture interacting using **REST APIs** the server is **Docker Engine** which sets at the background and takes care of building and running **Containers** a **Container** is a special kind of process **Containers** share the kernel of the host operating-system
**Note**: Kernel manages applications and hardware resources

## Installing the Docker

Download and install **Docker Desktop** application

`docker version` command to get docker info on your machine

```terminal
Client:
docker version

 Version:           27.2.0
 API version:       1.47
 Go version:        go1.21.13
 Git commit:        3ab4256
 Built:             Tue Aug 27 14:17:17 2024
 OS/Arch:           windows/amd64
 Context:           desktop-linux
```

## Docker Workflow

1. take an application and DOCKERIZE! it:
   - simply put a Dockerfile (a plain text file that contains instructions for docker) to it
2. give it to Docker for packaging our application into an Image
3. tell the Docker to start a container using that image

A Docker workflow typically involves a series of steps to develop, package, and deploy applications in isolated containers. Here’s an overview of the Docker workflow:

```docker
# typically start with a base image
# we can start with linux and add node on top of it
# or we can just start with node! which are build on top of linux distributions
# these images are all defined in the dockerhub
# node build on top of linux alpine distribution which results in a very small image file
FROM node:alpine
# here we say COPY all the files in the current directory into the app directory
# that image has a file-system and we're gonna create a directory called 'app'
COPY . /app
# here we specify the working directory to make file paths easier to work with
WORKDIR /app
# now using the CMD command we write the commands that start our application
# if we didn't specify the working-directory we had to write "CMD node app/app.js" because we've created an app directory withing that image
CMD node app.js
```

now that we have the **Dockerfile** we can tell the Docker to create an image of our application

in the terminal run `docker build -t image-name path-to-the-Dockerfile` for e,x: `docker build -t hello-docker .` when we're in the `docker-learning/hello-docker` folder path

the image file is not stored inside the project! it's Docker's business to store it!

to see all docker images on your machine in the terminal run `docker image ls` ls (list)

```terminal
PS D:\Courses\Docker\docker-learning> docker image ls
REPOSITORY         TAG       IMAGE ID       CREATED         SIZE
hello-docker-new   latest    8c4284648ad1   9 minutes ago   158MB
hello-docker       latest    ee4aa78d435d   2 hours ago     158MB
```

to run the image in the terminal run `docker run image-name` for e,x:

```terminal
PS D:\Courses\Docker\docker-learning> docker run hello-docker-new
Hello Docker!
```
