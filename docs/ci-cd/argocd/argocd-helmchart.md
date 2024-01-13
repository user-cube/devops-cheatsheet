---
title: ArgoCD HelmChart
layout: home
nav_order: 4
grand_parent: CI/CD
parent: ArgoCD
permalink: docs/cicd/arocd/helmchart
last_modified_date: 2024-01-13
---

# ArgoCD HelmChart

The ArgoCD HelmChart provides a convenient way to define and manage the deployment of ArgoCD within a Kubernetes cluster. It encapsulates the necessary configuration and resources required to deploy ArgoCD, including the definition of applications, management of source code, and automation of deployment processes. By using the HelmChart, users can easily deploy and manage ArgoCD in a consistent and reproducible manner.

## Table of Contents

- [ArgoCD HelmChart](#argocd-helmchart)
  * [Table of Contents](#table-of-contents)
  * [Add Helm](#add-helm)
  * [Install Helm](#install-helm)
  * [LDAP Integration](#ldap-integration)
    + [External Secrets](#external-secrets)
    + [LDAP Configuration](#ldap-configuration)
    + [LDAP Group Configurations](#ldap-group-configurations)
    + [UI Customization](#ui-customization)
      - [Personalized Banner](#personalized-banner)
      - [Personalized Logo](#personalized-logo)

## Add Helm

In order to add ArgoCD to our helms you need to execute the following command:

```bash
helm repo add argo https://argoproj.github.io/argo-helm
```

## Install Helm

To install you can execute the following command:

```bash
helm install argocd argo/argo-cd --version <desired-helm-version> -f values.yaml -n <desired-namespace>
```

## LDAP Integration

ArgoCD supports LDAP integration (using DEX), allowing users to authenticate and authorize against LDAP (Lightweight Directory Access Protocol) servers. This integration enables organizations to leverage their existing LDAP infrastructure for user management within ArgoCD.

To set up LDAP integration in ArgoCD, you would typically configure the LDAP settings in the ArgoCD configuration file or through the ArgoCD API. This involves specifying the LDAP server details, such as the server address, port, bind DN (Distinguished Name), and search base. Additionally, you would define the LDAP group settings to map LDAP groups to ArgoCD roles and permissions.

Once LDAP integration is configured, users can log in to ArgoCD using their LDAP credentials, and their access to ArgoCD resources can be controlled based on their LDAP group memberships.

You can find detailed information about ArgoCD LDAP Integration on our [dedicated section](/devops-cheatsheet/docs/cicd/argocd/ldap-integration).

### External Secrets

To manage secrets in Kubernetes, you can use the External Secrets controller. It allows you to store and manage secrets in external secret stores such as AWS Secrets Manager, HashiCorp Vault, or Azure Key Vault. The External Secrets controller retrieves the secrets from these external stores and injects them into your Kubernetes pods as environment variables or files. This helps in keeping sensitive information separate from your application code and configuration.

To deploy our secrets for LDAP Integration we can use the following secret:

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: ldap-external-secrets
spec:
  data:
  - remoteRef:
      conversionStrategy: Default
      key: kv/argocd/ldap
      property: ldap-bindDN
    secretKey: ldap-bindDN
  - remoteRef:
      conversionStrategy: Default
      key: kv/argocd/ldap
      property: ldap-bindPW
    secretKey: ldap-bindPW
  refreshInterval: 3600s
  secretStoreRef:
    kind: ClusterSecretStore
    name: vault-backend
  target:
    creationPolicy: Owner
    deletionPolicy: Retain
    name: ldap-external-secrets
```

### LDAP Configuration

This is a sample LDAP configuration for ArgoCD using DEX. Replace `<LDAP_URL>`, `<LDAP_USER_BASE_DN>`, and `<LDAP_GROUP_BASE_DN>` with your LDAP server details.

```yaml
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
```

### LDAP Group Configurations

Once the LDAP is integrated we can now set the permissions associated with the LDAP Groups, this can also be done in the helm by configuring the following parameters:

```yaml
# Argo CD RBAC policy configuration
## Ref: https://github.com/argoproj/argo-cd/blob/master/docs/operator-manual/rbac.md
rbac:
  # -- Create the argocd-rbac-cm configmap with ([Argo CD RBAC policy]) definitions.
  # If false, it is expected the configmap will be created by something else.
  # Argo CD will not work if there is no configmap created with the name above.
  create: true
 
  # -- Annotations to be added to argocd-rbac-cm configmap
  annotations: {}
 
  # -- The name of the default role which Argo CD will falls back to, when authorizing API requests (optional).
  # If omitted or empty, users may be still be able to login, but will see no apps, projects, etc...
  policy.default: 'role:readonly'
 
  # -- File containing user-defined policies and role definitions.
  # @default -- `''` (See [values.yaml])
  policy.csv: |
    p, role:devops-role, applications, *, */*, allow
    p, role:devops-role, clusters, *, *, allow
    p, role:devops-role, repositories, get, *, allow
    p, role:devops-role, repositories, create, *, allow
    p, role:devops-role, repositories, update, *, allow
    p, role:devops-role, repositories, delete, *, allow
    p, role:devops-role, applications, *, */*, allow
    p, role:devops-role, projects, *, *, allow
    p, role:infra-role, clusters, get, *, allow
    p, role:infra-role, repositories, get, *, allow
    p, role:infra-role, repositories, create, *, allow
    p, role:infra-role, repositories, update, *, allow
    p, role:infra-role, repositories, delete, *, allow
    p, role:developers-role, applications, create, */*, deny
    p, role:developers-role, applications, update, */*, allow
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
 
  # -- OIDC scopes to examine during rbac enforcement (in addition to `sub` scope).
  # The scope value can be a string, or a list of strings.
  scopes: "[groups,uid]"
```

### UI Customization

ArgoCD provides the ability to customize its user interface (UI) to meet specific requirements. UI customization in ArgoCD allows users to tailor the appearance and behavior of the interface to align with their organization's branding and user experience preferences. This can include customizing colors, logos, layout, and other visual elements to create a cohesive and personalized user interface for managing continuous delivery workflows.

#### Personalized Banner

To add a personalized banner to the ArgoCD UI, you can customize the UI by adding your organization's logo or any other personalized visual element to the interface. This can be achieved through the UI customization features provided by ArgoCD.

We can define a banner using the following configurations on the helmchart.

```yaml
## Argo Configs
configs:
  # General Argo CD configuration
  ## Ref: https://github.com/argoproj/argo-cd/blob/master/docs/operator-manual/argocd-cm.yaml
  cm:
    # -- Create the argocd-cm configmap for [declarative setup]
    create: true
 
    # -- Annotations to be added to argocd-cm configmap
    annotations: {}
 
    # -- Argo CD's externally facing base URL (optional). Required when configuring SSO
    url: "https://<ARGO_CD_URL>"
 
    # -- The name of tracking label used by Argo CD for resource pruning
    # @default -- Defaults to app.kubernetes.io/instance
    application.instanceLabelKey: argocd.argoproj.io/instance
 
    # -- Enable logs RBAC enforcement
    ## Ref: https://argo-cd.readthedocs.io/en/latest/operator-manual/upgrading/2.3-2.4/#enable-logs-rbac-enforcement
    server.rbac.log.enforce.enable: true
 
    # -- Enable exec feature in Argo UI
    ## Ref: https://argo-cd.readthedocs.io/en/latest/operator-manual/rbac/#exec-resource
    exec.enabled: false
 
    # -- Enable local admin user
    ## Ref: https://argo-cd.readthedocs.io/en/latest/faq/#how-to-disable-admin-user
    admin.enabled: true
 
    # -- Timeout to discover if a new manifests version got published to the repository
    timeout.reconciliation: 180s
 
    # -- Timeout to refresh application data as well as target manifests cache
    timeout.hard.reconciliation: 0s
 
    ui.bannercontent: "You are working on ArgoCD"
    ui.bannerpermanent: "true"
    ui.bannerposition: "top"
```

#### Personalized Logo

To add a personalized logo to the ArgoCD UI, you can utilize the UI customization features provided by ArgoCD. This will allow you to incorporate your organization's logo or any other personalized visual element into the interface.

```yaml
# -- Define custom [CSS styles] for your argo instance.
# This setting will automatically mount the provided CSS and reference it in the argo configuration.
# @default -- `""` (See [values.yaml])
## Ref: https://argo-cd.readthedocs.io/en/stable/operator-manual/custom-styles/
styles: |
  .login__logo img.logo-image {
    display: none
  }
  .login__logo {
      background-size: 200px 50px;
      background-image: url(<ADDRESS_TO_YOUR_LOGO>);
  }
```

