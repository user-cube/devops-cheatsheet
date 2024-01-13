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
If you are using LDAP, you should consider using the [LDAP Integration Page](/devops-cheatsheet/docs/cicd/argocd/ldap-integration) and utilize LDAP Groups and Users instead.
</div>

## Table of Contents

- [ArgoCD Create Local Users](#argocd-create-local-users)
  * [Table of Contents](#table-of-contents)
  * [Create a user in the config-map](#create-user-in-the-config-map)
  * [Define a new password](#define-a-new-password)
  * [Set permissions for users](#set-permissions-for-users)

## Create a user in the config-map

To create a new user, update the file `argocd-cm.yaml`. Open the file and make changes according to this example:

```yaml
apiVersion: v1
data:
  accounts.devops: apiKey,login
  accounts.tibco: apiKey,login
  accounts.<NEW_USER>: apiKey, login
  application.instanceLabelKey: argocd.argoproj.io/instance
```

## Define a new password

Execute the following command using the argocd CLI tool:

```bash
argocd account update-password --account <NEW_USER> --new-password "<NEW_PASSWORD>"
```

## Set permissions for users

To set permissions for users, update the file argocd-rbac.yaml. Open the file and make changes according to this example:

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
  policy.default: role:readonly
```

**Note**: If you want to create a read-only user, only add the line:

```yaml
g, <USER>, role:<NEW_ROLE>
```

You can learn more about permissions in the [ArgoCD Official Documentation](https://argo-cd.readthedocs.io/en/stable/operator-manual/rbac/).

