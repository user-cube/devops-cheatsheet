---
title: Kompose
layout: home
grand_parent: Tools & Tips
parent: Tools
nav_order: 2
permalink: docs/tols-and-tips/tools/kompose
last_modified_date: 2024-04-21
---

# Kompose

What is Kompose? It is a tool for converting Docker Compose files to Kubernetes or OpenShift resources.

For more information, visit the [official Kompose website](http://kompose.io).

Before starting, ensure that you have a Kubernetes cluster set up and the kubectl command-line tool configured to communicate with your cluster. It is recommended to run this tutorial on a cluster with at least two nodes that are not acting as control plane hosts. If you do not have a cluster, you can create one using minikube or use one of these Kubernetes playgrounds:
- [Play with Kubernetes](http://labs.play-with-k8s.com/)

To check the version, run `kubectl version`.

```bash
# Linux
curl -L https://github.com/kubernetes/kompose/releases/download/v1.26.0/kompose-linux-amd64 -o kompose
 
# macOS
curl -L https://github.com/kubernetes/kompose/releases/download/v1.26.0/kompose-darwin-amd64 -o kompose
 
# Windows
curl -L https://github.com/kubernetes/kompose/releases/download/v1.26.0/kompose-windows-amd64.exe -o kompose.exe
 
chmod +x kompose
sudo mv ./kompose /usr/local/bin/kompose
```
