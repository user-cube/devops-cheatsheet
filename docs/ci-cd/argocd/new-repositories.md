---
title: ArgoCD Add New Repositories
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
This process can be executed through the ArgoCD interface, but we prefer to store everything in our git repository (always use gitops if possible).
</div>

## Table of Contents

- [ArgoCD add new repositories](#argocd-add-new-repositories)
  * [Table of Contents](#table-of-contents)
  * [Add repositories on helm](#add-repositories-on-helm)
  * [Create credentials to access git repositories](#create-credentials-to-access-git-repositories)

## Add repositories on helm

In the helm values file, we need to add the repository we want to connect to ArgoCD:

```yaml
repositories:
  k8s-components:
    url: ssh://git@<repository_url>/devops/k8s_components.git
    type: git
    insecure: "true"
    project: default
    name: k8s-components
```

This will use the credentials below to grant access.

## Create credentials to access git repositories
<div markdown="block">
{: .important }
This step is only required once.
</div>

To retrieve content from git repositories, we need to create a set of credentials to be deployed on our cluster. These credentials are stored in our Vault and can be used across multiple git repositories.

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
Ensure that the `argocd.argoproj.io/secret-type: repo-creds` label is present for ArgoCD to recognize this as repository credentials.
With this secret, all repositories that start with the same content present in ssh-url-credentials will use this private key associated with the secret.
