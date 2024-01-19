---
title: Storage
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 7
last_modified_date: 2024-01-19
permalink: docs/kubernetes/cheatsheets/storage
---

# Storage in Kubernetes

Kubernetes provides a variety of storage solutions to meet the needs of applications with different storage requirements. It supports both local storage, for single node usage, and network storage (or shared storage), which can be used by multiple nodes.

## Table of Contents

- [Storage in Kubernetes](#storage-in-kubernetes)
    * [Table of Contents](#table-of-contents)
    * [Why is Storage Important in Kubernetes?](#why-is-storage-important-in-kubernetes)
    * [Creating Persistent Volumes](#creating-persistent-volumes)
    * [Using Persistent Volumes](#using-persistent-volumes)
    * [Storage Limitations](#storage-limitations)
    * [Cheat Sheets](#cheat-sheets)

## Why is Storage Important in Kubernetes?

Storage in Kubernetes allows data to persist even when the container, pod, or the worker node is removed. It decouples the life of the data being stored from the life of the pod.

## Creating Persistent Volumes

You can create Persistent Volumes using the `kubectl apply -f` with a Persistent Volume YAML, or via the Kubernetes API.

## Using Persistent Volumes

Persistent Volumes provide an API for users and administrators that abstracts details of how storage is provided from how it is consumed.

## Storage Limitations

The implementation of Persistent Volumes in Kubernetes has certain limitations. For example, Persistent Volumes are cluster resources and not namespaced. 

## Cheat Sheets

| Name                                                                                   | Command                                                                                                      |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Create a Persistent Volume                                                             | `kubectl apply -f persistentvolume.yaml`                                                                    |
| Get Persistent Volumes                                                                 | `kubectl get persistentvolumes`                                                                              |
| Describe a Persistent Volume                                                           | `kubectl describe persistentvolume <NAME>`                                                                  |
| Delete a Persistent Volume                                                             | `kubectl delete persistentvolume <NAME>`                                                                    |
| Get a Persistent Volume's capacity field                                               | `kubectl get persistentvolume <NAME> -o jsonpath='{.spec.capacity}'`                                         |
| Get a Persistent Volume's specific capacity field                                      | `kubectl get persistentvolume <NAME> -o jsonpath='{.spec.capacity.<KEY>}'`                                   |
| Patch a Persistent Volume                                                              | `kubectl patch persistentvolume <NAME> -p '{"spec":{"capacity":{"storage":"new value"}}}'`                   |
| Replace a Persistent Volume                                                            | `kubectl replace -f persistentvolume.yaml`                                                                  |