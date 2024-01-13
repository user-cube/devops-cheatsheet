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
Effective July 2023, Compose V1 stopped receiving updates and is no longer in new Docker Desktop releases. Compose V2 has replaced it and is now integrated into all current Docker Desktop versions. For more information, see [Migrate to Compose V2](https://docs.docker.com/compose/migrate/).
</div>

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration.

Compose works in all environments; production, staging, development, testing, as well as CI workflows. It also has commands for managing the whole lifecycle of your application:

- Start, stop, and rebuild services
- View the status of running services
- Stream the log output of running services
- Run a one-off command on a service

 
## Install Docker Compose

To install Docker Compose, follow the instructions below based on your operating system:

- **Linux**: 
  - To install Docker Compose on Linux, please visit [Linux Install](https://docs.docker.com/desktop/install/linux-install/) for detailed installation steps.

- **MacOS**: 
  - For MacOS, detailed installation instructions for Docker Compose can be found at [Mac Install](https://docs.docker.com/desktop/install/mac-install/).

- **Windows**: 
  - Detailed installation steps for Docker Compose on Windows can be found at [Windows Install](https://docs.docker.com/desktop/install/windows-install/).

