---
title: Dockerfiles
layout: home
nav_order: 1
parent: Docker
has_children: true
permalink: docs/docker/dockerfiles
last_modified_date: 2024-01-08
---

# Dockerfiles

Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. This page describes the commands you can use in a Dockerfile.

## Overview
The Dockerfile supports the following instructions:

| Instruction | Description                                                 |
|-------------|-------------------------------------------------------------|
| ADD         | Add local or remote files and directories.                  |
| ARG         | Use build-time variables.                                   |
| CMD         | Specify default commands.                                   |
| COPY        | Copy files and directories.                                 |
| ENTRYPOINT  | Specify default executable.                                 |
| ENV         | Set environment variables.                                  |
| EXPOSE      | Describe which ports your application is listening on.      |
| FROM        | Create a new build stage from a base image.                 |
| HEALTHCHECK | Check a container's health on startup.                      |
| LABEL       | Add metadata to an image.                                   |
| MAINTAINER  | Specify the author of an image.                             |
| ONBUILD     | Specify instructions for when the image is used in a build. |
| RUN         | Execute build commands.                                     |
| SHELL       | Set the default shell of an image.                          |
| STOPSIGNAL  | Specify the system call signal for exiting a container.     |
| USER        | Set user and group ID.                                      |
| VOLUME      | Create volume mounts.                                       |
| WORKDIR     | Change working directory.                                   |

