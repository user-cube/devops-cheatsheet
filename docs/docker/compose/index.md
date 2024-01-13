---
title: Docker Compose
layout: home
nav_order: 1
parent: Docker
has_children: true
permalink: docs/docker/compose
last_modified_date: 2024-01-13
---

# Docker Compose

<div markdown="block">
{: .important }
Docker's documentation refers to and describes Compose V2 functionality. <br>
As of July 2023, Compose V1 has ceased to receive updates and is no longer included in new Docker Desktop releases. Compose V2 has replaced it and is now integrated into all current Docker Desktop versions. For more information, see [Migrate to Compose V2](https://docs.docker.com/compose/migrate/).
</div>

Docker Compose is a tool for defining and running multi-container Docker applications. It uses a YAML file to configure application services. With a single command, all the services from the configuration can be created and started.

Docker Compose works in various environments, including production, staging, development, testing, and CI workflows. It also provides commands for managing the entire lifecycle of applications:

- Start, stop, and rebuild services
- View the status of running services
- Stream the log output of running services
- Run a one-off command on a service

 
## Install Docker Compose

To install Docker Compose, follow the instructions below based on your operating system:

- **Linux**: 
  - For detailed installation steps on Linux, visit [Linux Install](https://docs.docker.com/desktop/install/linux-install/).

- **MacOS**: 
  - Detailed installation instructions for Docker Compose on MacOS can be found at [Mac Install](https://docs.docker.com/desktop/install/mac-install/).

- **Windows**: 
  - Detailed installation steps for Docker Compose on Windows can be found at [Windows Install](https://docs.docker.com/desktop/install/windows-install/).

```
