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

Docker uses a **Client/Server** architecture interacting using **REST APIs** the server is **Docker Engine** which sets at the background and takes care of building and running **Containers** a **Container** is a special kind of process
