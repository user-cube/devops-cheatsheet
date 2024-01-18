---
title: Deployments
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 3
last_modified_date: 2024-01-18
---

# Deployments in Kubernetes

A Deployment in Kubernetes provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. Deployments are defined using YAML (preferred) or JSON, like all Kubernetes objects.

## Table of Contents

- [Deployments in Kubernetes](#deployments-in-kubernetes)
  * [Table of Contents](#table-of-contents)
  * [Why Use a Deployment?](#why-use-a-deployment)
  * [Creating Deployments](#creating-deployments)
  * [Updating Deployments](#updating-deployments)
  * [Rolling Back a Deployment](#rolling-back-a-deployment)
  * [Scaling a Deployment](#scaling-a-deployment)
  * [Cheat Sheets](#cheat-sheets)

## Why Use a Deployment?

Deployments are crucial when you want to ensure that a specified number of identical Pods are always up and running. They allow for easy updating of Pods without causing downtime by incrementally updating Pods instances with new ones.

## Creating Deployments

You can create a Deployment by defining a .yaml or .json file and using `kubectl apply -f` command.

## Updating Deployments

You can update a Deployment by applying a new .yaml or .json file with the updated configuration. The Deployment will ensure that the Pods transition to the new state while maintaining the desired number of Pods.

## Rolling Back a Deployment

If an update to a Deployment is not stable, you can roll back to a previous state easily using the `kubectl rollout undo` command.

## Scaling a Deployment

You can scale the number of Pods in a Deployment using the `kubectl scale` command or by updating the .yaml or .json file.

![Kubernetes Deployments](https://user-cube.github.io/devops-cheatsheet/assets/images/kubernetes/deployments.svg)

## Cheat Sheets

| Name                                                                                   | Command                                                                                                      |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| List all deployments                                                                   | `kubectl get deployments`                                                                                    |
| List all deployments for all namespaces                                                | `kubectl get deployments -A`                                                                                 |
| List all deployments in ps output format with more information (such as node name)     | `kubectl get deployments -o wide`                                                                            |
| Get deployment configurations as yaml                                                  | `kubectl get deployment <NAME> -o yaml`                                                                      |
| Get deployment information                                                             | `kubectl describe deployment/<NAME>`                                                                         |
| List a single deployment with specified NAME in ps output format                       | `kubectl get deployment <NAME>`                                                                              |
| List all deployments with labels                                                       | `kubectl get deployments --show-labels`                                                                      |
| List deployments in JSON output format, in the "v1" version of the "apps" API group    | `kubectl get deployments.v1.apps -o json`                                                                    |
| List a single deployment in JSON output format                                         | `kubectl get -o json deployment/<NAME>`                                                                      |
| List a deployment identified by type and name specified in "deployment.yaml" in JSON   | `kubectl get -f deployment.yaml -o json`                                                                     |
| List resources from a directory with kustomization.yaml - e.g. dir/kustomization.yaml  | `kubectl get -k dir/`                                                                                        |
| Scale a deployment                                                                     | `kubectl scale deployment/<NAME> --replicas=<NUMBER>`                                                        |
| Rollout status of a deployment                                                         | `kubectl rollout status deployment/<NAME>`                                                                   |
| Rollback a deployment                                                                  | `kubectl rollout undo deployment/<NAME>`                                                                     |
| List deployment information in custom columns                                          | `kubectl get deployment NAME -o custom-columns=READY:.status.readyReplicas,UPDATED:.status.updatedReplicas`  |
| List all replication controllers, services and deployments together in ps output format| `kubectl get rc,services,deployments`                                                                        |
| List one or more resources by their type and names                                     | `kubectl get rc/<NAME> service/<NAME> deployment/<NAME>`                                                     |