---
title: Pods
layout: home
parent: Kubernetes Cheat Sheets
nav_order: 1
last_modified_date: 2024-01-07
---

# Kubernetes Pods

## Table of Contents

- [Kubernetes Pods](#kubernetes-pods)
  * [Table of Contents](#table-of-contents)
  * [Cheat Sheet](#cheat-sheet)
- [Kubernetes Pods Overview](#kubernetes-pods-overview)

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
| Get Pod initContainer status                                                          | `kubectl get pod --template '{{.status.initContainerStatuses}}' <NAME>`                                     |
| List a single pod in JSON output format                                               | `kubectl get -o json <NAME>`                                                                                |
| List a pod identified by type and name specified in "pod.yaml" in JSON output format  | `kubectl get -f pod.yaml -o json`                                                                           |
| List resources from a directory with kustomization.yaml - e.g. dir/kustomization.yaml | `kubectl get -k dir/`                                                                                       |
| Return only the phase value of the specified pod                                      | `kubectl get -o template pod/<NAME> --template={{.status.phase}}`                                           |
| List resource information in custom columns                                           | `kubectl get pod NAME -o custom-columns=CONTAINER:.spec.containers[0].name,IMAGE:.spec.containers[0].image` |
| List all replication controllers and services together in ps output format            | `kubectl get rc,services`                                                                                   |
| List one or more resources by their type and names                                    | `kubectl get rc/<NAME> service/<NAME> pods/<NAME>`                                                          |
| Run command on a running pod                                                          | `kubectl exec -it <NAME> -- <COMMAND_TO_BE_EXECUTED>`                                                       |

# Kubernetes Pods Overview

A Pod is a Kubernetes abstraction that represents a group of one or more application containers (such as Docker), and some shared resources for those containers. Those resources include:

- Shared storage, as Volumes
- Networking, as a unique cluster IP address
- Information about how to run each container, such as the container image version or specific ports to use

A Pod models an application-specific "logical host" and can contain different application containers which are relatively tightly coupled. For example, a Pod might include both the container with your Node.js app as well as a different container that feeds the data to be published by the Node.js webserver. The containers in a Pod share an IP Address and port space, are always co-located and co-scheduled, and run in a shared context on the same Node.

Pods are the atomic unit on the Kubernetes platform. When we create a Deployment on Kubernetes, that Deployment creates Pods with containers inside them (as opposed to creating containers directly). Each Pod is tied to the Node where it is scheduled, and remains there until termination (according to restart policy) or deletion. In case of a Node failure, identical Pods are scheduled on other available Nodes in the cluster.

![Pods Overview](../../assets/images/pods.svg)