---
title: Test Playbooks On Docker
layout: home
nav_order: 1
grand_parent: Ansible
parent: Ansible Playbooks
permalink: docs/ansible/playbooks/test-on-docker
last_modified_date: 2024-01-13
---

# Test Playbooks On Docker

To test Ansible playbooks on Docker, you can use a Dockerfile to create a Docker image with Ansible installed. Then, you can run a container based on that image and execute your playbooks inside the container. Here's a basic example of a Dockerfile that installs Ansible:

```Dockerfile
FROM ubuntu:latest

RUN apt-get update \
    && apt-get install --no-install-recommends -y python3-pip \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install pip --upgrade
RUN pip3 install ansible

RUN apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    sshpass

WORKDIR /work
```

You can build the Docker image using the docker build command and then run a container based on that image. Inside the container, you can execute your Ansible playbooks using the ansible-playbook command.

```bash
docker build -t ansible:ubuntu-latest .
docker run  -v "${PWD}":/work:ro -v ~/.ansible/roles:/root/.ansible/roles -v ~/.ssh:/root/.ssh:ro --rm ansible ansible-playbook playbook.yaml
```

You can find more information about this dockerfile on our [documentation](/docs/docker/dockerfiles/ansible).