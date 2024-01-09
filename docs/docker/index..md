---
title: Docker
layout: home
nav_order: 5
has_children: true
permalink: docs/docker
last_modified_date: 2024-01-08
---

# Docker

Docker is a platform for developing, shipping, and running applications in containers. Containers are lightweight, portable, and self-sufficient units that can run applications and their dependencies isolated from the host system. Docker provides a way to package and distribute applications along with their dependencies in a consistent and reproducible manner.

Below are some key concepts and commands related to Docker

## Image

An image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools.

- Pull an image from Docker Hub:

```bash
docker pull IMAGE_NAME[:TAG]
```

- List locally available images:

```bash
docker images
```

## Container

A container is a running instance of a Docker image. It is an isolated environment that runs applications and their dependencies.

- Run a container from an image:

```bash
docker run IMAGE_NAME[:TAG]
```

- List running containers:

```bash
docker ps
```

- List all containers (including stopped ones):

```bash
docker ps -a
```

## Dockerfile

A Dockerfile is a script that contains instructions for building a Docker image. It specifies the base image, sets up the environment, and defines how to run the application.

- Example Dockerfile:

```Dockerfile
Copy code
FROM ubuntu:latest
RUN apt-get update && apt-get install -y my_package
CMD ["my_command"]
```

- Build an image from a Dockerfile:

```bash
docker build -t IMAGE_NAME[:TAG] PATH_TO_DOCKERFILE
```
## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It uses a YAML file to configure the application's services, networks, and volumes.

- Example docker-compose.yml:

```yaml
Copy code
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
```

- Run a Docker Compose application:

```bash
docker-compose up
```

## Docker Hub

Docker Hub is a cloud-based registry service that allows you to share and distribute Docker images. It is the default registry for Docker.

- Push an image to Docker Hub:

```bash
docker push USERNAME/IMAGE_NAME[:TAG]
```

- Pull an image from Docker Hub:

```bash
docker pull USERNAME/IMAGE_NAME[:TAG]
```

These are just basic commands and concepts to get you started with Docker. Docker provides a powerful and flexible environment for containerization, making it easier to manage and deploy applications across different environments.