---
title: Pods
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 1
last_modified_date: 2024-01-19
permalink: docs/kubernetes/cheatsheets/pods
---

# Pods in Kubernetes

A Pod is a Kubernetes abstraction that represents a group of one or more application containers (such as Docker), and some shared resources for those containers. Those resources include:

- Shared storage, as Volumes
- Networking, as a unique cluster IP address
- Information about how to run each container, such as the container image version or specific ports to use

A Pod models an application-specific "logical host" and can contain different application containers which are relatively tightly coupled. For example, a Pod might include both the container with your Node.js app as well as a different container that feeds the data to be published by the Node.js webserver. The containers in a Pod share an IP Address and port space, are always co-located and co-scheduled, and run in a shared context on the same Node.

Pods are the atomic unit on the Kubernetes platform. When we create a Deployment on Kubernetes, that Deployment creates Pods with containers inside them (as opposed to creating containers directly). Each Pod is tied to the Node where it is scheduled, and remains there until termination (according to restart policy) or deletion. In case of a Node failure, identical Pods are scheduled on other available Nodes in the cluster.

![Pods Overview](https://user-cube.github.io/devops-cheatsheet/assets/images/kubernetes/pods.svg)

## Table of Contents

- [Kubernetes Pods](#kubernetes-pods)
  * [Table of Contents](#table-of-contents)
  * [Why Use a Pod?](#why-use-a-pod)
  * [Creating Pods](#creating-pods)
  * [Using Pods](#using-pods)
  * [Pod Limitations](#pod-limitations)
  * [Cheat Sheet](#cheat-sheet)
  
## Why Use a Pod?

Pods allow you to manage, deploy and scale applications easily. They can be easily managed by Deployment, DaemonSet, Job, and other higher-level constructs.

## Creating Pods

You can create Pods using the `kubectl run` command, `kubectl apply -f` with a Pod YAML, or via the Kubernetes API.

## Using Pods

Pods can be used to host applications, temporary workloads, replicated applications, and more.

## Pod Limitations

Pods are ephemeral and do not have the capability to heal themselves in case of failures. They are designed to be disposable and replaceable.

## Cheat Sheet

| Name                                                                                  | Command                                                                                                     |
|---------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| List all pods                                                                         | `kubectl get pods`                                                                                          |
| List all pods for all namespaces                                                      | `kubectl get pods -A`                                                                                       |
| List all pods in ps output format with more information (such as node name)           | `kubectl get pods -o wide`                                                                                  |
| Get pod configurations as yaml                                                        | `kubectl get pod <NAME> -o yaml`                                                                            |
| Get pod information                                                                   | `kubectl describe pod/<NAME>`                                                                               |
| List a single replication controller with specified NAME in ps output format          | `kubectl get replicationcontroller <NAME>`                                                                  |
| List all pods with labels                                                             | `kubectl get pods --show-labels`                                                                            |
| List deployments in JSON output format, in the "v1" version of the "apps" API group   | `kubectl get deployments.v1.apps -o json`                                                                   |
| List unhealthy pods                                                                   | `kubectl get pods --field-selector=status.phase!=Running`                                                   |
| List unhealthy pods in all namespaces                                                 | `kubectl get pods --field-selector=status.phase!=Running -A`                                                |
| List running pods                                                                     | `kubectl get pods --field-selector=status.phase=Running`                                                    |
| List running pods in all namespaces                                                   | `kubectl get pods --field-selector=status.phase=Running -A`                                                 |
| Get Pod initContainer status                                                          | `kubectl get pod --template {% raw %}'{{.status.initContainerStatuses}}'{% endraw %} <NAME>`                |
| List a single pod in JSON output format                                               | `kubectl get -o json <NAME>`                                                                                |
| List a pod identified by type and name specified in "pod.yaml" in JSON output format  | `kubectl get -f pod.yaml -o json`                                                                           |
| List resources from a directory with kustomization.yaml - e.g. dir/kustomization.yaml | `kubectl get -k dir/`                                                                                       |
| Return only the phase value of the specified pod                                      | `kubectl get -o template pod/<NAME> {% raw %}--template={{.status.phase}} {% endraw %}`                     |
| List resource information in custom columns                                           | `kubectl get pod NAME -o custom-columns=CONTAINER:.spec.containers[0].name,IMAGE:.spec.containers[0].image` |
| List all replication controllers and services together in ps output format            | `kubectl get rc,services`                                                                                   |
| List one or more resources by their type and names                                    | `kubectl get rc/<NAME> service/<NAME> pods/<NAME>`                                                          |
| Run command on a running pod                                                          | `kubectl exec -it <NAME> -- <COMMAND_TO_BE_EXECUTED>`                                                       |