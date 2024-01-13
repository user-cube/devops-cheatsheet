---
title: ArgoCD Create Local Users
layout: home
nav_order: 2
grand_parent: CI/CD
parent: ArgoCD
permalink: docs/cicd/argocd/local-users
last_modified_date: 2024-01-13
---

# ArgoCD Create Local Users

<div markdown="block">
{: .important }
If you are using LDAP you should take a look at [LDAP Integration Page](/devops-cheatsheet/docs/cicd/argocd/ldap-integration), use LDAP Groups and Users instead. <br>
This procedure was replaced with LDAP user integrations, you can see this in more details on confluence: ArgoCD LDAP Integration
</div>

## Table of Contents

- [ArgoCD Create Local Users](#argocd-create-local-users)
  * [Table of Contents](#table-of-contents)
  * [Create user on config-map](#create-user-on-config-map)
  * [Define new password](#define-new-password)
  * [Set permissions to users](#set-permissions-to-users)

## Create user on config-map

In order to create a new user you need to update the file `argocd-cm.yaml`. Open the file and change according to this example:

```yaml
apiVersion: v1
data:
  accounts.devops: apiKey,login
  accounts.tibco: apiKey,login
  accounts.<NEW_USER>: apiKey, login
  application.instanceLabelKey: argocd.argoproj.io/instance
```

## Define new password

Execute the following command using argocd cli tool:

```bash
argocd account update-password --account <NEW_USER> --new-password "<NEW_PASSWORD>"
```

## Set permissions to users

In order to set permissions to users you need to update the file argocd-rbac.yaml. Open the file and change according to this example:

```yaml
apiVersion: v1
data:
  policy.csv: |
    p, role:devops-role, applications, *, */*, allow
    p, role:devops-role, clusters, get, *, allow
    p, role:devops-role, repositories, get, *, allow
    p, role:devops-role, repositories, create, *, allow
    p, role:devops-role, repositories, update, *, allow
    p, role:devops-role, repositories, delete, *, allow
    g, devops, role:devops-role
    g, tibco, role:tibco-role
  policy.default: role:readonly
```

**Note**: If you want to create a read-only user please only add the line:

```yaml
g, <USER>, role:<NEW_ROLE>
```

You can learn more about permissions in [ArgoCD Official Documentation](https://argo-cd.readthedocs.io/en/stable/operator-manual/rbac/).


