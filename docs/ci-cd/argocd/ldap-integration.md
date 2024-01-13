---
title: ArgoCD LDAP Integration
layout: home
nav_order: 4
grand_parent: CI/CD
parent: ArgoCD
permalink: docs/cicd/argocd/ldap-integration
last_modified_date: 2024-01-13
---

# ArgoCD LDAP Integration

<div markdown="block">
{: .important }
To set up LDAP integration in ArgoCD, you can configure these settings using the HelmChart. For detailed configuration options, please refer to our [ArgoCD HelmChart Page](/devops-cheatsheet/docs/cicd/argocd/helmchart). However, this section provides a detailed description of the integration.
</div>


ArgoCD supports LDAP integration (using DEX), allowing users to authenticate and authorize against LDAP (Lightweight Directory Access Protocol) servers. This integration enables organizations to leverage their existing LDAP infrastructure for user management within ArgoCD.

To set up LDAP integration in ArgoCD, you would typically configure the LDAP settings in the ArgoCD configuration file or through the ArgoCD API. This involves specifying the LDAP server details, such as the server address, port, bind DN (Distinguished Name), and search base. Additionally, you would define the LDAP group settings to map LDAP groups to ArgoCD roles and permissions.

Once LDAP integration is configured, users can log in to ArgoCD using their LDAP credentials, and their access to ArgoCD resources can be controlled based on their LDAP group memberships.

## Table of Contents

- [ArgoCD LDAP Integration](#argocd-ldap-integration)
  * [Table of Contents](#table-of-contents)
  * [Prepare secrets](#prepare-secrets)
  * [Dex configuration](#dex-configuration)
  * [Restart Services](#restart-services)
  * [Define policies for user groups](#define-policies-for-user-groups)

## Prepare secrets

First we need to create our LDAP secrets in order to configure LDAP. Pick LDAP Bind Password and LDAP Bind DN. You can do that by executing the following command:

```bash
echo "INSERT_BIND_DN_HERE" | base64
 
echo "INSERT_BIND_PASSWORD_HERE" | base64
```

After that you need to update argo secrets. You can edit the secrets by executing the following command:

```bash
kubectl edit secrets argocd-secret -n argocd
 
apiVersion: v1
data:
  dex.ldap.bindDN: <BASE_64_BIND_DN>
  dex.ldap.bindPW: <BASE_64_BIND_PASSWORD>
kind: Secret
```

Save the changes and they will persist into the Kubernetes cluster.

## Dex configuration

Once you have you secrets created you need to configure Dex. To configure Dex you execute the following command and edit the file content like this:

```bash
kubectl edit configmaps argocd-cm -n argocd
```

The dex configuration should look like this:

```yaml
apiVersion: v1
data:
  dex.config: |
    connectors:
    - type: ldap
      name: LDAP
      id: ldap
      config:
        # Ldap server address
        host: "<LDAP_URL>"
        insecureNoSSL: true
        insecureSkipVerify: true
        # Variable name stores ldap bindDN in argocd-secret
        bindDN: "$dex.ldap.bindDN"
        # Variable name stores ldap bind password in argocd-secret
        bindPW: "$dex.ldap.bindPW"
        usernamePrompt: Username
        # Ldap user search attributes
        userSearch:
          baseDN: "<LDAP_USER_BASE_DN>"
          filter: ""
          username: sAMAccountName
          idAttr: sAMAccountName
          emailAttr: mail
          nameAttr: givenName
        # Ldap group search attributes
        groupSearch:
          baseDN: "<LDAP_GROUP_BASE_DN>"
          filter: "(objectClass=group)"
          userAttr: DN
          groupAttr: member
          nameAttr: cn
  url: https://<YOUR_ARGOCD_URL>
```

Make sure you have `url` on your yaml definition otherwise Argo won't redirect you after a login is done.
You can save the file and it should be applied to the Kubernetes cluster.

**Note**: To reload configurations you don't need to delete the pods, dex will automatically reload LDAP configurations.

## Restart Services

Now that everything is configured you need to restart ArgoCD services, you can do it by executing the following command:

```bash
kubectl delete po -l app.kubernetes.io/component=server  -n argocd                                                                                                          
kubectl delete po -l app.kubernetes.io/component=dex-server  -n argocd
```

A new button will apear on the interface:

![argocd](https://user-cube.github.io/devops-cheatsheet/assets/images/argocd/ldap-button.png)

After you press that button you will be redirected to a login page:

![argocd](https://user-cube.github.io/devops-cheatsheet/assets/images/argocd/dex-ldaplogin.png)

This page is using LDAP to perform the action. Since we changed the logging to debug you will be able to see some logs about the operations being done in dex server:

```bash
kubectl logs deployment.apps/argocd-dex-server -f
 
time="2022-11-22T09:58:08Z" level=info msg="performing ldap search ****** (sAMAccountName=*****)"
time="2022-11-22T09:58:08Z" level=info msg="username \"*****\" mapped to entry CN=*****,*******""
time="2022-11-22T09:58:08Z" level=info msg="performing ldap search ****** (&(objectClass=group)(******))"
time="2022-11-22T09:58:08Z" level=info msg="login successful: connector \"ldap\", username=\"****\", preferred_username=\"\", email=\"******\", groups=[\"DEVOPS\" \"INFRA\" \"ADMIN\"]"
time="2022-11-22T09:58:08Z" level=info msg="performing ldap search ****** (sAMAccountName=*****)"
time="2022-11-22T09:58:08Z" level=info msg="username \"*****\" mapped to entry CN=*****,*******"
time="2022-11-22T09:58:08Z" level=info msg="performing ldap search ****** (&(objectClass=group)(member=CN=*****,*******))"
time="2022-11-22T09:58:08Z" level=info msg="login successful: connector \"ldap\", username=\"******\", preferred_username=\"\", email=\"******\", groups=[\"DEVOPS\" \"INFRA\" \"ADMIN\"]"
```

## Define policies for user groups

The LDAP integration is now working, you need to set permissions according to groups and roles, you can do this by editing the configmap with all security policies.

```bash
kubectl edit configmaps argocd-rbac-cm -n argocd
```

You can define the policies like this:

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
    p, role:devops-role, applications, *, */*, allow
    p, role:infra-role, clusters, get, *, allow
    p, role:infra-role, repositories, get, *, allow
    p, role:infra-role, repositories, create, *, allow
    p, role:infra-role, repositories, update, *, allow
    p, role:infra-role, repositories, delete, *, allow
    p, role:developers-role, applications, create, */*, deny
    p, role:developers-role, applications, update, */*, deny
    p, role:developers-role, applications, delete, */*, allow
    p, role:developers-role, applications, sync, */*, allow
    p, role:developers-role, applications, override, */*, deny
    p, role:developers-role, applications, action/*, */*, allow
    p, role:developers-role, applicationsets, get, */*, allow
    p, role:developers-role, applicationsets, create, */*, deny
    p, role:developers-role, applicationsets, update, */*, deny
    p, role:developers-role, applicationsets, delete, */*, deny
    p, role:developers-role, certificates, create, *, deny
    p, role:developers-role, certificates, update, *, deny
    p, role:developers-role, certificates, delete, *, deny
    p, role:developers-role, clusters, create, *, deny
    p, role:developers-role, clusters, update, *, deny
    p, role:developers-role, clusters, delete, *, deny
    p, role:developers-role, repositories, create, *, deny
    p, role:developers-role, repositories, update, *, deny
    p, role:developers-role, repositories, delete, *, deny
    p, role:developers-role, projects, create, *, deny
    p, role:developers-role, projects, update, *, deny
    p, role:developers-role, projects, delete, *, deny
    p, role:developers-role, accounts, update, *, deny
    p, role:developers-role, gpgkeys, create, *, deny
    p, role:developers-role, gpgkeys, delete, *, deny
    p, role:developers-role, exec, create, */*, deny
    g, DEVOPS, role:devops-role
    g, DEVELOPERS, role:developers-role
    g, INFRA, role:infra-role
  policy.default: role:readonly
  scopes: '[groups,uid]'
```

You need to define the field scopes and the field that adds the group user to the role: g, LDAP_GROUP_USER, role:ROLE_NAME.