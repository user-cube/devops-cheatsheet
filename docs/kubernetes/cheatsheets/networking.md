---
title: Networking
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 6
last_modified_date: 2024-01-19
permalink: docs/kubernetes/cheatsheets/networking
---

# Networking in Kubernetes

Networking is a central part of Kubernetes, but it can be challenging to understand exactly how it is expected to work. There are 4 distinct networking problems to address: 

1. Highly-coupled container-to-container communications
2. Pod-to-Pod communications
3. Pod-to-Service communications
4. External-to-Service communications

![Kubernetes Networking](https://user-cube.github.io/devops-cheatsheet/assets/images/kubernetes/networking.svg)

## Table of Contents

- [Networking in Kubernetes](#networking-in-kubernetes)
    * [Table of Contents](#table-of-contents)
    * [Why is Networking Important in Kubernetes?](#why-is-networking-important-in-kubernetes)
    * [Creating Network Policies](#creating-network-policies)
    * [Using Network Policies](#using-network-policies)
    * [Networking Limitations](#networking-limitations)
    * [Cheat Sheets](#cheat-sheets)

## Why is Networking Important in Kubernetes?

Networking in Kubernetes provides the communication path between different components. It ensures that these components can communicate with each other and with other applications or systems.

## Creating Network Policies

You can create Network Policies using the `kubectl apply -f` with a Network Policy YAML, or via the Kubernetes API.

## Using Network Policies

Network Policies specify how groups of pods are allowed to communicate with each other and other network endpoints.

## Networking Limitations

Network Policies are implemented by the network plugin, so you must be using a networking solution which supports NetworkPolicy.

## Cheat Sheets

| Name                                                                                   | Command                                                                                                      |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Create a Network Policy                                                                | `kubectl apply -f networkpolicy.yaml`                                                                        |
| Get Network Policies                                                                   | `kubectl get networkpolicies`                                                                                |
| Describe a Network Policy                                                              | `kubectl describe networkpolicy <NAME>`                                                                      |
| Delete a Network Policy                                                                | `kubectl delete networkpolicy <NAME>`                                                                        |
| Get a Network Policy's podSelector field                                               | `kubectl get networkpolicy <NAME> -o jsonpath='{.spec.podSelector}'`                                         |
| Get a Network Policy's specific podSelector field                                      | `kubectl get networkpolicy <NAME> -o jsonpath='{.spec.podSelector.<KEY>}'`                                   |
| Patch a Network Policy                                                                 | `kubectl patch networkpolicy <NAME> -p '{"spec":{"podSelector":{"key":"new value"}}}'`                       |
| Replace a Network Policy                                                               | `kubectl replace -f networkpolicy.yaml`                                                                      |