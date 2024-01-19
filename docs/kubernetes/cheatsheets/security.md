---
title: Security
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 8
last_modified_date: 2024-01-19
permalink: docs/kubernetes/cheatsheets/security
---

# Security in Kubernetes

Kubernetes provides many built-in security features to help you protect your cluster, and your applications. These include network policies, TLS for secure communication, secret management, RBAC, security context, and more.

## Table of Contents

- [Security in Kubernetes](#security-in-kubernetes)
    * [Table of Contents](#table-of-contents)
    * [Why is Security Important in Kubernetes?](#why-is-security-important-in-kubernetes)
    * [Creating Network Policies](#creating-network-policies)
    * [Using RBAC](#using-rbac)
    * [Security Limitations](#security-limitations)
    * [Cheat Sheets](#cheat-sheets)

## Why is Security Important in Kubernetes?

Security in Kubernetes is important to protect sensitive data, meet regulatory compliance, and ensure uninterrupted services.

## Creating Network Policies

You can create Network Policies using the `kubectl apply -f` with a Network Policy YAML, or via the Kubernetes API.

## Using RBAC

Role-Based Access Control (RBAC) in Kubernetes enables administrators to dynamically configure policies through the Kubernetes API.

## Security Limitations

While Kubernetes provides many built-in security features, it is not a silver bullet and requires configuration and maintenance to ensure a secure environment.

## Cheat Sheets

| Name                                                                                   | Command                                                                                                      |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Create a Network Policy                                                                | `kubectl apply -f networkpolicy.yaml`                                                                        |
| Get Network Policies                                                                   | `kubectl get networkpolicies`                                                                                |
| Describe a Network Policy                                                              | `kubectl describe networkpolicy <NAME>`                                                                      |
| Delete a Network Policy                                                                | `kubectl delete networkpolicy <NAME>`                                                                        |
| Create a Role                                                                          | `kubectl create role <NAME> --verb=<VERBS> --resource=<RESOURCES>`                                           |
| Create a RoleBinding                                                                   | `kubectl create rolebinding <NAME> --role=<ROLE_NAME> --user=<USER_NAME>`                                    |
| Get Roles                                                                              | `kubectl get roles`                                                                                          |
| Get RoleBindings                                                                       | `kubectl get rolebindings`                                                                                   |
| Describe a Role                                                                        | `kubectl describe role <NAME>`                                                                               |
| Describe a RoleBinding                                                                 | `kubectl describe rolebinding <NAME>`                                                                        |
| Delete a Role                                                                          | `kubectl delete role <NAME>`                                                                                 |
| Delete a RoleBinding                                                                   | `kubectl delete rolebinding <NAME>`                                                                          |