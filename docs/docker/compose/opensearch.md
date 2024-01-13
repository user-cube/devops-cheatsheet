---
title: OpenSearch Compose File
layout: home
nav_order: 4
grand_parent: Docker
parent: Docker Compose
permalink: docs/docker/compose/opensearch
last_modified_date: 2024-01-13
---

# OpenSearch Compose File

OpenSearch is a powerful, open-source search and analytics engine. It is known for its scalability, speed, and comprehensive feature set, making it suitable for handling diverse search and analytics workloads. OpenSearch supports various data types, advanced querying capabilities, and features such as full-text search, aggregations, and analytics.

OpenSearch is commonly used for log and event data analysis, full-text search applications, and real-time analytics. It is well-suited for use cases that require distributed search and analytics, complex querying, and near real-time data insights. Additionally, it provides extensibility through plugins, custom analyzers, and data visualization tools.

![opensearch](https://user-cube.github.io/devops-cheatsheet/assets/images/docker/open-search-logo.png)

## Table of Contents

- [OpenSearch Compose File](#opensearch-compose-file)
  * [Table of Contents](#table-of-contents)
  * [Compose file](#compose-file)
  * [Flag DISABLE_SECURITY_PLUGIN](#flag-disable_security_plugin)
  * [Step by Step](#step-by-step)

## Compose file

```yaml
version: '3'

services:
  opensearch:
    image: opensearchproject/opensearch:1.0.0
    container_name: opensearch-container
    environment:
      - cluster.name=my-opensearch-cluster
      - node.name=my-opensearch-node
      - discovery.type=single-node
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    ports:
      - "9200:9200"
      - "9300:9300"
    volumes:
      - opensearch-data:/usr/share/opensearch/data

volumes:
  opensearch-data:
```

The provided Docker Compose file sets up a service for OpenSearch, an open-source search and analytics engine. It defines the configuration for running OpenSearch in a Docker environment. The file specifies the image, container name, environment variables, ulimits, port mappings, and volumes required for the OpenSearch service.

This configuration allows for the deployment of OpenSearch with specific settings for cluster and node names, memory allocation, and data persistence. Additionally, it exposes the necessary ports for accessing OpenSearch and sets up memory lock ulimits for the container.

## Flag DISABLE_SECURITY_PLUGIN

The `DISABLE_SECURITY_PLUGIN=true` environment variable is used to disable the security plugin in OpenSearch. This may be necessary in certain development or testing scenarios where you want to run OpenSearch without security features enabled.

In a production environment or any scenario where data security is a concern, it's important to configure and enable appropriate security measures for OpenSearch to protect sensitive data and ensure secure access to the search and analytics engine.

It's crucial to carefully consider the implications of disabling the security plugin and to only do so in environments where it is appropriate and necessary for the specific use case.

This flag is very usefull if you are plugins like [ElasticVue](https://elasticvue.com/) for you local deployments. Elasticvue is a free and open-source elasticsearch gui for the browser.

## Step by Step

1. Version: The version field specifies the version of the Docker Compose file format being used, in this case, version 3.

2. Services: Under the services section, a service named "opensearch" is defined.

- Image: It uses the "opensearchproject/opensearch:1.0.0" image.
- Container Name: The container_name field sets the name of the container to "opensearch-container".
- Environment: Environment variables are set for the cluster name, node name, discovery type, memory lock, and Java options.
- Ulimits: It sets memory lock ulimits for the container.
- Ports: Port mapping is set to allow access to OpenSearch on ports 9200 and 9300.
- Volumes: A volume named "opensearch-data" is mounted into the container for data persistence.

3. Volumes: The volumes section defines the "opensearch-data" volume used by the "opensearch" service for data persistence.