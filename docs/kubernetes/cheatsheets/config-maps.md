---
title: ConfigMaps
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 4
last_modified_date: 2024-01-19
permalink: docs/kubernetes/cheatsheets/config-maps
---

# ConfigMaps in Kubernetes

A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

## Table of Contents

- [ConfigMaps in Kubernetes](#configmaps-in-kubernetes)
  * [Table of Contents](#table-of-contents)
  * [Why Use a ConfigMap?](#why-use-a-configmap)
  * [Creating ConfigMaps](#creating-configmaps)
  * [Using ConfigMaps](#using-configmaps)
  * [ConfigMap Limitations](#configmap-limitations)
  * [Cheat Sheets](#cheat-sheets)

## Why Use a ConfigMap?

ConfigMaps allow you to decouple configuration artifacts from image content to keep containerized applications portable. This separation of data from code allows your application to be deployed alongside its configuration.

## Creating ConfigMaps

You can create ConfigMaps using the `kubectl create configmap` command, `kubectl apply -f` with a ConfigMap YAML, or via the Kubernetes API.

## Using ConfigMaps

You can use a ConfigMap in a Pod spec wherever environment variables are called for, or as a file in a Pod's volume.

## ConfigMap Limitations

ConfigMaps are not suitable for storing sensitive information. Use a Secret for that.

## Cheat Sheets

| Name                                                                                   | Command                                                                                                      |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Create a new ConfigMap                                                                 | `kubectl create configmap <NAME> --from-literal=key=value`                                                   |
| Create a new ConfigMap from a file                                                     | `kubectl create configmap <NAME> --from-file=path/to/file`                                                   |
| Get ConfigMaps                                                                         | `kubectl get configmaps`                                                                                     |
| Describe a ConfigMap                                                                   | `kubectl describe configmap <NAME>`                                                                          |
| Delete a ConfigMap                                                                     | `kubectl delete configmap <NAME>`                                                                            |
| Get a ConfigMap's data field                                                           | `kubectl get configmap <NAME> -o jsonpath='{.data}'`                                                         |
| Get a ConfigMap's specific data field                                                  | `kubectl get configmap <NAME> -o jsonpath='{.data.<KEY>}'`                                                   |
| Patch a ConfigMap                                                                      | `kubectl patch configmap <NAME> -p '{"data":{"key":"new value"}}'`                                           |
| Replace a ConfigMap                                                                    | `kubectl replace -f configmap.yaml`                                                                          |