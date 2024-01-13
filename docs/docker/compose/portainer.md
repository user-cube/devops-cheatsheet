---
title: Portainer Compose File
layout: home
nav_order: 1
grand_parent: Docker
parent: Docker Compose
permalink: docs/docker/compose/portainer
last_modified_date: 2024-01-13
---

# Portainer Compose File

Portainer is a lightweight management UI which allows you to easily manage your Docker host or Swarm cluster. It is designed to be as simple to deploy as it is to use. Portainer consists of a single container that can run on any Docker engine. Portainer allows you to manage your Docker containers, images, volumes, networks, and more. It is compatible with standalone Docker environments as well as Docker Swarm clusters.

Portainer is a great tool for managing your Docker environment through a user-friendly interface. It provides a visual representation of the Docker environment, making it easier to monitor and manage containers, images, and other resources. With Portainer, you can easily create and manage containers, inspect container logs, and monitor resource usage. Additionally, Portainer offers role-based access control, allowing you to define user roles and permissions for managing Docker resources. Whether you are a beginner or an experienced Docker user, Portainer simplifies the management of Docker environments and provides a seamless user experience.

## Table of contents

- [Portainer Compose File](#portainer-compose-file)
  * [Table of contents](#table-of-contents)
  * [Compose file](#compose-file)
    + [Step by step](#step-by-step)

## Compose file

Here is a Docker Compose file to deploy Portainer:

```yaml
version: '3.8'
services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    command: -H unix:///var/run/docker.sock
    ports:
      - "9000:9000"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
      - "portainer_data:/data"
    restart: always
volumes:
  portainer_data:
```

The provided Docker Compose file deploys Portainer, a lightweight management UI for Docker. It specifies a service named "portainer" using the "portainer/portainer-ce:latest" image, with port mapping from host port 9000 to container port 9000. It also mounts the Docker socket and a volume for data persistence. The service is set to restart unless stopped. This Compose file is written in version 3.8 of the Docker Compose format.

### Step by step

1. The version field specifies the version of the Docker Compose file format being used, in this case, version 3.8.

2. Under the services section, a service named "portainer" is defined. It uses the "portainer/portainer-ce:latest" image, which is the latest version of the Portainer Community Edition.

3. The container_name field sets the name of the container to "portainer".

4. The command field specifies the command to be executed when the container starts. In this case, it sets the Docker host to use the Unix socket at "/var/run/docker.sock".

5. The ports field maps port 9000 on the host to port 9000 in the container, allowing access to the Portainer UI.

6. The volumes field mounts two volumes into the container. The first volume mounts the Docker socket from the host to the container, allowing Portainer to interact with the Docker engine. The second volume creates a persistent volume named "portainer_data" for storing Portainer's data.

7. The restart field specifies the restart policy for the container. In this case, the container will restart unless explicitly stopped.

8. Finally, the volumes section defines the "portainer_data" volume used by the "portainer" service for data persistence.

