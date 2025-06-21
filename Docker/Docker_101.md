# Docker 101

> References: [Docker Official Docs](https://docs.docker.com/get-started/overview/)

## What is Docker?

- A **platform-as-a-service that creates isolated virtualization environments** for building, implementing, and testing applications
- When using Docker, you can separate applications from infrastructure to run software quickly

<br/>

## Docker Structure

![docker_structure.png](/images/docker_structure.png)

- Docker uses a client-server architecture.
- **Docker client** communicates with **Docker Daemon** which performs heavy tasks like building, running, and deploying Docker Containers.
- Uses Linux Kernel features to create Containers on top of the operating system, and Docker itself runs as a Daemon that manages service Containers.
- The **Docker server** is the entity that actually creates Containers and manages Images, and operates in the Docker engine process.
- Docker engine receives API input from outside and performs Docker engine functions.
- The state where Docker process is running and **ready to receive input as a server** is called Docker Daemon
- When you enter commands starting with `docker`, you're using the Docker client.
- Docker client passes the entered commands as API to the Docker Daemon that exists locally
- At this time, Docker client calls Docker Daemon's API through a socket located at /var/run/docker.sock

<br/>

## What is Container?

- Provides functionality to deliver applications in **consistent, standardized form** like containers used in actual cargo ships
- Provides functionality to package and run applications in loosely isolated environments
- Can run multiple Containers simultaneously on a specified host through isolation and security
- Lightweight and includes everything needed to run applications, so no need to depend on items installed on the host. In other words, everyone gets the same Container that works the same way
- Therefore, Docker **allows developers to work in standardized environments using local Containers that provide applications and services**.
- Containers are also suitable for CI/CD workflows

<br/>

## What is Daemon?

- Receives Docker API requests and manages Docker objects such as Images, Containers, networks, and volumes.
- Daemon can also communicate with other Daemons to manage Docker services.

<br/>

## What is Image?

- Used for packaging and transporting applications.
- Includes independent environment needed to run applications, and can be seen as a **kind of template for runtime environment**.
- It's an immutable file that includes source code, libraries, dependencies, tools, and other files needed to run applications.
- Images are read-only, so they're also called snapshots, representing applications and virtual environments at a specific point in time.
- This consistency is one of Docker's major features, allowing developers to test and experiment with software in stable and uniform environments
