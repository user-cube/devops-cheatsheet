---
title: ArgoCD add new repositories
layout: home
nav_order: 3
grand_parent: CI/CD
parent: ArgoCD
permalink: docs/cicd/argocd/new-repositories
last_modified_date: 2024-01-13
---

# ArgoCD add new repositories

<div markdown="block">
{: .important }
This procedure can be done using ArgoCD interface but in our case we want to save everything on our git repository (always use gitops if possible).
</div>

## Table of Contents

- [ArgoCD add new repositories](#argocd-add-new-repositories)
  * [Table of Contents](#table-of-contents)
  * [Add repositories on helm](#add-repositories-on-helm)
  * [Create credentials to access git repositories](#create-credentials-to-access-git-repositories)

## Add repositories on helm

On the helm values file we need to add the repository we want to be connected on ArgoCD:

```yaml
repositories:
  dgl-k8s-components:
    url: ssh://git@<repository_url>/devops/dgl_k8s_components.git
    type: git
    insecure: "true"
    project: default
    name: dgl-k8s-components
```

This will use the credentials below in order to grant access.

## Create credentials to access git repositories
<div markdown="block">
{: .important }
This step is only required to be done only once
</div>

In order to be able to get content from git repositories we need to create a set of credentials to be deployed on our cluster. This credentials are stored on our Vault and can be used across all multiple git repositories.

This secret should be placed under a repository that will be activated on ArgoCD as an external secret provider.

```yaml
---
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: git-credentials
  namespace: argocd
spec:
  data:
  - remoteRef:
      conversionStrategy: Default
      key: kv/argocd/repositories
      property: ssh-private-key
    secretKey: sshPrivateKey
  - remoteRef:
      conversionStrategy: Default
      key: kv/argocd/repositories
      property: ssh-url-credentials
    secretKey: url
  refreshInterval: 3600s
  secretStoreRef:
    kind: ClusterSecretStore
    name: vault-backend
  target:
    creationPolicy: Owner
    deletionPolicy: Retain
    name: git-credentials
    template:
      metadata:
        labels:
          argocd.argoproj.io/secret-type: repo-creds
```
Make sure you have `argocd.argoproj.io/secret-type: repo-creds` label in order to ArgoCD detect this as credentials for repositories.
With this secret all repositories that starts with the same content present on ssh-url-credentials will be using this private key associated with the secret.