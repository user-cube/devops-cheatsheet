---
title: Run containers with SSL
layout: home
nav_order: 1
parent: Docker
permalink: docs/docker/run-with-ssl
last_modified_date: 2024-01-13
---

# Run containers with SSL

Secure Sockets Layer (SSL) is a standard security technology for establishing an encrypted link between a server and a client. In the context of Docker, SSL can be used to secure the communication between Docker containers and clients that connect to them.

![ssl](https://user-cube.github.io/devops-cheatsheet/assets/images/docker/ssl.jpeg)

## Table of Contents

- [Run containers with SSL](#run-containers-with-ssl)
  * [Table of Contents](#table-of-contents)
  * [Setting up SSL on Docker Containers](#setting-up-ssl-on-docker-containers)
    + [Install mkcert](#install-mkcert)
      - [MacOs](#macos)
      - [Linux (Ubuntu/Debian based)](#linux-ubuntudebian-based)
      - [Windows](#windows)
    + [Install CA on your machine](#install-ca-on-your-machine)
    + [Generate certificate](#generate-certificate)
    + [Prepare nginx](#prepare-nginx)
      - [Break down nginx configuration](#break-down-nginx-configuration)
    + [Add nginx to compose file](#add-nginx-to-compose-file)

## Setting up SSL on Docker Containers

To set up SSL on Docker containers, you typically need to create a self-signed SSL certificate and configure your Docker container to use it. Here's a basic step-by-step guide.

### Install mkcert

#### MacOs
```bash
brew install mkcert
```

#### Linux (Ubuntu/Debian based)

```bash
curl -JLO "https://dl.filippo.io/mkcert/latest?for=linux/amd64"
chmod +x mkcert-v*-linux-amd64
sudo cp mkcert-v*-linux-amd64 /usr/local/bin/mkcert
```

#### Windows

```shell
choco install mkcert
```

### Install CA on your machine

```bash
mkcert -install
```

### Generate certificate

```bash
mkcert localhost 127.0.0.1 ::1

Created a new certificate valid for the following names 📜
 - "localhost"
 - "127.0.0.1"
 - "::1"

The certificate is at "./localhost+2.pem" and the key at "./localhost+2-key.pem" ✅

It will expire on 22 April 2026 🗓
```

### Prepare nginx

Create the following directories on your `docker-compose` file location:

```bash
mkdir -p proxy/certs
mkdir -p proxy/conf
```

Place the certificates under `proxy/certs`. 

Add your nginx configuration to `proxy/conf/nginx.conf`:

```nginx
worker_processes 1;

events {
    worker_connections 1024;
}

http {
    server {
        listen 443 ssl;
        server_name localhost;

        ssl_certificate /etc/nginx/certs/localhost+2.pem;
        ssl_certificate_key /etc/nginx/certs/localhost+2-key.pem;

        location / {
            proxy_pass http://my-service:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
```

#### Break down nginx configuration

- `worker_processes 1;`: This sets the number of worker processes. In this case, it's set to 1.

- `events { worker_connections 1024; }`: This block configures the events module. The `worker_connections` directive sets the maximum number of simultaneous connections that can be opened by a worker process.

- `http { ... }`: This block is where the main configuration for handling HTTP and HTTPS requests is done.

- `server { ... }`: This block defines a server that listens on the SSL port (443) and responds to requests for the specified `server_name` (localhost in this case).

- `listen 443 ssl;`: This tells Nginx to listen on port 443 with SSL.

- `ssl_certificate /etc/nginx/certs/localhost+2.pem;`: This specifies the location of the SSL certificate file.

- `ssl_certificate_key /etc/nginx/certs/localhost+2-key.pem;`: This specifies the location of the SSL certificate key file.

- `location / { ... }`: This block defines how to respond to requests for the root URL ("/"). In this case, it's set up to proxy these requests to another service.

- `proxy_pass http://my-service:8080;`: This line tells Nginx to forward the incoming requests to the service running at `http://my-service:8080`.

- The `proxy_set_header` directives are used to add HTTP headers to the request that is forwarded to the proxied service. This is useful for letting the proxied service know about the original request's details.

Make sure you update `listen 443 ssl;` to use the port you want to communicate with your service.

Make sure you update `proxy_pass http://my-service:8080;` with the name of your service present on the `docker-compose` file.

### Add nginx to compose file

Add nginx to docker-compose:

```yaml
version: '3'

services:
  proxy:
    image: nginx:latest
    ports:
      - 9200:9200
    volumes:
      - ./proxy/conf/nginx.conf:/etc/nginx/nginx.conf
      - ./proxy/certs:/etc/nginx/certs 
  my-service:
    image: my-service:latest
    ports:
      - 80:80
```