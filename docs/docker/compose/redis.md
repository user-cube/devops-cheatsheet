---
title: Redis Compose File
layout: home
nav_order: 2
grand_parent: Docker
parent: Docker Compose
permalink: docs/docker/compose/databases/redis
last_modified_date: 2024-01-13
---

# Redis Compose File

Redis is an open-source, in-memory data structure store, used as a database, cache, and message broker. It supports various data structures such as strings, hashes, lists, sets, and more. Redis is commonly used for caching, session management, real-time analytics, message queuing, and pub/sub messaging.

Redis should be used when fast read and write operations are required, and when data needs to be stored in memory for quick access. It is suitable for use cases such as real-time analytics, high-speed transactions, caching frequently accessed data, and managing session data in web applications.

![redis](https://user-cube.github.io/devops-cheatsheet/assets/images/docker/redis-logo.png)

## Table of contents

- [Redis Compose File](#redis-compose-file)
  * [Table of contents](#table-of-contents)
  * [Compose file](#compose-file)
    + [Step by step](#step-by-step)

## Compose file

```yaml
version: '3.8'
services:
  redis:
    image: "redis:6.2"
    container_name: "<CONTAINER_NAME>"
    ports:
      - "6379:6379"  # host_port:container_port
    volumes:
      - redis-data:/data
    environment:
      - REDIS_PASSWORD=<REDIS_PASSWORD>
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 3

volumes:
  redis-data:
```

The provided Docker Compose file defines a service for Redis using version 6.2 of the Redis image. It sets up port mapping for accessing the Redis server, mounts a volume for data persistence, and defines an environment variable for the Redis password. Additionally, it includes a health check configuration for the Redis service.

### Step by step

1. The version field specifies the version of the Docker Compose file format being used, in this case, version 3.8.

2. Under the services section, a service named "redis" is defined. It uses the "redis:6.2" image, which is the version 6.2 of Redis.

3. The container_name field sets the name of the container to "<CONTAINER_NAME>".

4. The ports field maps port 6379 on the host to port 6379 in the container, allowing access to the Redis server.

5. The volumes field mounts a volume named "redis-data" into the container for data persistence.

6. The environment field sets the environment variable "REDIS_PASSWORD" to "<REDIS_PASSWORD>".

7. The healthcheck section defines a health check for the "redis" service, which pings the Redis server using "redis-cli" and expects a "pong" response within a specified interval, timeout, and number of retries.

8. Finally, the volumes section defines the "redis-data" volume used by the "redis" service for data persistence.
