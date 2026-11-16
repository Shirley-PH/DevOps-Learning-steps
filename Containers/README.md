# Docker Fundamentals

This document explains the basic concepts of Docker in a simple and practical way. The goal is to make the topic easy to understand for people who are not experts in technology while still showing the commands used in real projects.

## What is Docker?

Docker is a tool that helps developers package an application and everything it needs to run, such as libraries, dependencies, and configuration files, into a single unit called an image.

Think of it as putting an application in a portable box. That box can run the same way on a laptop, a server, or in the cloud, without depending on the machine's local configuration.

In simple words:
- An image is the blueprint.
- A container is the running version of that blueprint.


## Docker Hub

Docker Hub is a public registry where developers can find and share ready-to-use images.

Website: https://hub.docker.com/

This is useful because, instead of creating everything from scratch, you can download a base image such as Nginx, MySQL, or Node.js and use it directly.

## Common Docker commands

### 1. Run a container

The command below downloads and runs the official hello-world image.

```bash
docker run hello-world
```

This command creates a container from the image and executes it.

### 2. List downloaded images

```bash
docker images
```

This shows all the images available locally on the machine.

### 3. List containers

```bash
docker ps -a
```

This shows all containers, including those that are stopped. The `-a` flag means "all".

## Example: running Nginx in a container

The following command creates a container named `web01` and runs Nginx in the background.

```bash
docker run --name web01 -d -p 9080:80 nginx
```

Explanation:
- `docker run`: creates and starts a container
- `--name web01`: gives the container a custom name
- `-d`: runs the container in the background (detached mode)
- `-p 9080:80`: maps ports from the local machine to the container
- `nginx`: the image to use

Port mapping means:
- `9080` is the port on your computer
- `80` is the port inside the container

So, if you open a browser and go to `http://localhost:9080`, you are accessing the Nginx service inside the container.

## Inspecting a container

To check the details of a running or stopped container, use:

```bash
docker inspect web01
```

This command shows technical information such as:
- container ID
- network configuration
- assigned IP address
- environment variables
- volumes and ports

This is useful when you want to verify how the container is configured.

## Pulling an image

Docker images are often downloaded from Docker Hub before they are used.

```bash
docker pull nginx
```

This downloads the Nginx image to your local environment. Once downloaded, it can be used multiple times.

## Building an image from a Dockerfile

A Dockerfile is a text file that contains instructions for creating an image. It defines what should be installed and how the application should run.

```bash
docker build
```

### Common options

- `-t nameTest`: assigns a name to the image
- `.`: tells Docker to use the current directory as the build context

Example:

```bash
docker build -t testimg .
```

This command reads the Dockerfile in the current folder and creates an image named `testimg`.

## Running a container from a custom image

Once the image is built, it can be started with:

```bash
docker run -P -d testimg
docker ps
```

Explanation:
- `docker run`: creates and starts the container
- `-P`: publishes the ports declared in the Dockerfile
- `-d`: runs in the background
- `testimg`: the custom image we created earlier
- `docker ps`: lists the running containers

## Cleaning up Docker resources

As you work with Docker, containers and images can accumulate. It is important to remove unused ones to keep the system organized.

### Stop a container

```bash
docker ps
docker stop name1 name2 name3
```

This stops one or more containers.

### Remove an image

```bash
docker images
docker rmi imageID imageID
```

`docker rmi` removes images, while `docker stop` stops containers. It is important to understand the difference:
- a container is a running object
- an image is a reusable template

## Learning progress

This project has helped me understand:
- how to build Docker images
- how to run containers
- how to expose ports
- how to inspect container details
- how to manage images and containers

This demonstrates a practical understanding of Docker and its role in application deployment and environment consistency.
