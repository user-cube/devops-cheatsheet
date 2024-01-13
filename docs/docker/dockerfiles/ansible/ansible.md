---
title: Ansible Playbooks on Docker
layout: home
nav_order: 1
grand_parent: Docker
parent: Dockerfiles
permalink: docs/docker/dockerfiles/ansible
last_modified_date: 2024-01-13
---

# Ansible Playbooks on Docker

To test Ansible playbooks on Docker, you can use a Dockerfile to create a Docker image with Ansible installed. Then, you can run a container based on that image and execute your playbooks inside the container. Here's a basic example of a Dockerfile that installs Ansible:

## Table of Content

- [Ansible Playbooks on Docker](#ansible-playbooks-on-docker)
  * [Table of Content](#table-of-content)
  * [Dockerfile](#dockerfile)
  * [Build and run docker image](#build-and-run-docker-image)
  * [Step by Step](#step-by-step)

## Dockerfile

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

## Build and run docker image

```bash
docker build -t ansible:ubuntu-latest .
docker run  -v "${PWD}":/work:ro -v ~/.ansible/roles:/root/.ansible/roles -v ~/.ssh:/root/.ssh:ro --rm ansible ansible-playbook playbook.yaml ;
```

## Step by Step

Here is a step-by-step breakdown of the Dockerfile:

1. It starts with a base image ubuntu:latest.
2. It updates the package list and installs python3-pip without recommended packages.
3. It upgrades pip and installs ansible.
4. It updates the package list again, and installs sshpass without recommended packages.
5. Finally, it sets the working directory to /work.

This Dockerfile sets up an environment with Ubuntu, Python, Pip, Ansible, and SSHpass.