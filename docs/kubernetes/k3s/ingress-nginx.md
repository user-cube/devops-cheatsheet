---
title: Ingress Nginx on K3S
layout: home
nav_order: 1
grand_parent: Kubernetes
parent: K3S
permalink: docs/kubernetes/k3s/ingress-nginx
last_modified_date: 2024-04-21
---

# Ingress Nginx on K3S

Ingress Nginx is a powerful tool for managing external access to services in a Kubernetes cluster. This guide will walk you through the process of installing and configuring Ingress Nginx on a K3S cluster.

## What is Ingress Nginx?

Ingress Nginx is a Kubernetes Ingress controller that uses ConfigMap to store the nginx configuration. It's one of the implementations of the Kubernetes Ingress system, which is a way to manage external access to services in a cluster.

## Installing Ingress Nginx on K3S

You can install Ingress Nginx on K3S using Helm, a package manager for Kubernetes. Here's how:

```bash
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```

If you don't want to use helm you can use nginx installation for bare-metal:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/baremetal/deploy.yaml
```

## K3S on AWS Machines

In case you are running K3S on a EC2 machine in order to expose the ingress you will need to update `externalIPs` on your service configuration, execute:

```bash
kubectl edit svc ingress-nginx -n ingress-nginx
```

And the following content:

```yaml
spec:
  - 80.11.12.10
```