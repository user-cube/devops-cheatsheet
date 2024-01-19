---
title: Secrets
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 5
last_modified_date: 2024-01-19
permalink: docs/kubernetes/cheatsheets/secrets
---

# Secrets in Kubernetes

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in an image. Using Secrets gives you control over how sensitive data is used and reduces the risk of accidental exposure.

## Table of Contents

- [Secrets in Kubernetes](#secrets-in-kubernetes)
    * [Table of Contents](#table-of-contents)
    * [Why Use a Secret?](#why-use-a-secret)
    * [Creating Secrets](#creating-secrets)
    * [Using Secrets](#using-secrets)
    * [Secret Limitations](#secret-limitations)
    * [Cheat Sheets](#cheat-sheets)

## Why Use a Secret?

Secrets offer a more secure and flexible way to store and manage sensitive information, such as passwords, OAuth tokens, and ssh keys, in Kubernetes.

## Creating Secrets

You can create Secrets using the `kubectl create secret` command, `kubectl apply -f` with a Secret YAML, or via the Kubernetes API.

## Using Secrets

You can use a Secret in a Pod spec wherever sensitive data is called for, or as a file in a Pod's volume.

## Secret Limitations

Secrets are stored in TempFS on a node and are sent to a node only if a Pod on that node requires it. It remains until the Pod is deleted.

## Cheat Sheets

| Name                                                                                   | Command                                                                                                      |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Create a new Secret                                                                    | `kubectl create secret generic <NAME> --from-literal=key=value`                                              |
| Create a new Secret from a file                                                        | `kubectl create secret generic <NAME> --from-file=path/to/file`                                              |
| Get Secrets                                                                            | `kubectl get secrets`                                                                                        |
| Describe a Secret                                                                      | `kubectl describe secret <NAME>`                                                                             |
| Delete a Secret                                                                        | `kubectl delete secret <NAME>`                                                                               |
| Get a Secret's data field                                                              | `kubectl get secret <NAME> -o jsonpath='{.data}'`                                                            |
| Get a Secret's specific data field                                                     | `kubectl get secret <NAME> -o jsonpath='{.data.<KEY>}'`                                                      |
| Patch a Secret                                                                         | `kubectl patch secret <NAME> -p '{"data":{"key":"new value"}}'`                                              |
| Replace a Secret                                                                       | `kubectl replace -f secret.yaml`                                                                             |