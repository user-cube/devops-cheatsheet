---
title: Postgres Compose File
layout: home
nav_order: 3
grand_parent: Docker
parent: Docker Compose
permalink: docs/docker/compose/databases/postgres
last_modified_date: 2024-01-13
---

# Postgres Compose File

PostgreSQL is a powerful, open-source object-relational database system. It is known for its reliability, robust feature set, and ability to handle complex workloads. PostgreSQL supports various data types, indexing techniques, and advanced features such as full-text search and JSON support.

PostgreSQL is commonly used for web applications, data warehousing, and geospatial applications. It is suitable for use cases that require ACID compliance, complex queries, and high data integrity. Additionally, it provides extensibility through custom functions, procedural languages, and custom data types.

![postgres](https://user-cube.github.io/devops-cheatsheet/assets/images/docker/postgres-logo.png)

## Table of Contents

- [Postgres Compose File](#postgres-compose-file)
  * [Table of Contents](#table-of-contents)
  * [Compose file](#compose-file)
    + [Step by step](#step-by-step)

## Compose file

```yml
version: '3.8'

services:
  postgres:
    image: "postgres:16.1"  # Use a specific version for stability
    container_name: "postgres-container"
    restart: always
    ports:
      - "5432:5432"
    environment:
      POSTGRES_DB: <POSTGRES_DATABASE_NAME>
      POSTGRES_USER: <POSTGRES_DATABASE_USER>
      POSTGRES_PASSWORD: <POSTGRES_PASSWORD>
      PGDATA: /var/lib/postgresql/data/pgdata
      POSTGRES_INITDB_ARGS: "--data-checksums"
    volumes:
      - postgres-data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD", "pg_isready", "-q", "-d", "<POSTGRES_DATABASE_NAME>", "-U", "<POSTGRES_DATABASE_USER>"]
      interval: 10s
      timeout: 5s
      retries: 3

volumes:
  postgres-data:
```

The provided Docker Compose file defines a service for PostgreSQL using the version 13 of the PostgreSQL image. It sets up port mapping for accessing the PostgreSQL server, mounts a volume for data persistence, and defines environment variables for the PostgreSQL database name, user, password, data directory, and initialization arguments. Additionally, it includes a health check configuration for the PostgreSQL service.

### Step by step

1. The version field specifies the version of the Docker Compose file format being used, in this case, version 3.8.

2. Under the services section, a service named "postgres" is defined. It uses the "postgres:16.1" image, which is a specific version for stability.

3. The container_name field sets the name of the container to "postgres-container".

4. The restart field specifies the restart policy for the container. In this case, the container will always restart unless explicitly stopped.

5. The ports field maps port 5432 on the host to port 5432 in the container, allowing access to the PostgreSQL server.

6. The environment field sets environment variables for the PostgreSQL database name, user, password, data directory, and initialization arguments.

7. The volumes field mounts a volume named "postgres-data" into the container for data persistence.

8. The healthcheck section defines a health check for the "postgres" service, which checks the readiness of the PostgreSQL server using "pg_isready" command with specified interval, timeout, and number of retries.

9. Finally, the volumes section defines the "postgres-data" volume used by the "postgres" service for data persistence.
