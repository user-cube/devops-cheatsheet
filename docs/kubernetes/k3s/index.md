---
title: K3S
layout: home
nav_order: 1
parent: Kubernetes
has_children: true
permalink: docs/kubernetes/k3s
last_modified_date: 2024-01-07
---

# K3S

K3s is a lightweight Kubernetes distribution designed for edge computing, IoT, and resource-constrained environments. It provides a simplified, easy-to-install Kubernetes platform without compromising on essential Kubernetes features. K3s is known for its small footprint, efficient resource usage, and streamlined installation process, making it well-suited for scenarios where traditional Kubernetes may be too resource-intensive or complex to deploy.

K3s can be installed with access to the KUBECONFIG file using specific installation commands, and it also allows customization of features such as the default ingress class. Additionally, it provides options for setting up the `KUBECONFIG` file and configuring various aspects of the Kubernetes environment.


## Avoid permissions error on KUBECONFIG

In order to install K3S with access to the KUBECONFIG file execute the instalation as follows:

```bash
curl -sfL <https://get.k3s.io> | sh -s - --write-kubeconfig-mode 644
# or
curl -sfL <https://get.k3s.io> | K3S_KUBECONFIG_MODE="644" sh -s -
```

## Ingress Class

By default K3S uses Traefik as default ingress class so, if you want don't want to install Traefik you should perform your installation using the following command:

```bash
curl -sfL <https://get.k3s.io> | K3S_KUBECONFIG_MODE="644" INSTALL_K3S_VERSION="v1.22.17+k3s1" INSTALL_K3S_EXEC="--disable=traefik" sh -s -
```

## Setup KUBECONFIG file

In order to setup the KUBECONFIG file you can execute the following command:

```bash
cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
```
