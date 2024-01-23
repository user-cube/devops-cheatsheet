---
title: ArgoCD
layout: home
nav_order: 1
parent: CI/CD
has_children: true
permalink: docs/cicd/argocd
last_modified_date: 2024-01-13
---

# ArgoCD

ArgoCD is a declarative, GitOps continuous delivery tool for Kubernetes. It automates the deployment of applications and configurations to Kubernetes clusters by using Git repositories as the source of truth. ArgoCD continuously monitors the desired state in the Git repository and reconciles any differences with the actual state in the Kubernetes cluster.

With ArgoCD, users can define applications, their associated Kubernetes resources, and configurations in a Git repository. ArgoCD then ensures that the applications are deployed and maintained according to the definitions in the repository, providing a consistent and auditable deployment process.

ArgoCD also offers a web-based user interface for visualizing and managing the deployed applications, as well as a CLI and API for automation and integration with other tools.

![argocd](https://user-cube.github.io/devops-cheatsheet/assets/images/argocd/argocd-logo.png)