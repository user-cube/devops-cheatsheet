---
title: Sonarqube
layout: home
nav_order: 6
permalink: docs/sonarqube
last_modified_date: 2024-01-13
---

# Sonarqube

SonarQube is an open-source platform for continuous code quality inspection. It performs static code analysis to identify bugs, code smells, and security vulnerabilities in various programming languages. SonarQube seamlessly integrates with build systems and code repositories to automatically assess code quality during the development process.

Supporting a wide array of programming languages, SonarQube provides comprehensive reports on code quality metrics, including code duplication, complexity, and test coverage. It also offers security-focused analysis to pinpoint potential vulnerabilities within the codebase.

Development teams rely on SonarQube to uphold and enhance their code quality, ensuring compliance with industry standards and best practices. By integrating SonarQube into the development workflow, teams can proactively detect and address code quality issues, resulting in more dependable and secure software.


![sonarqube](https://user-cube.github.io/devops-cheatsheet/assets/images/sonarqube/sonarqube-logo.png)

## Table of Contents

- [Sonarqube](#sonarqube)
  * [Table of Contents](#table-of-contents)
  * [LDAP Integration](#ldap-integration)
    + [Vault](#vault)
    + [Create external secret](#create-external-secret)
    + [Update sonarqube helm](#update-sonarqube-helm)

## LDAP Integration

To integrate SonarQube with LDAP, specific parameters need to be defined in the Sonar configuration. As LDAP contains sensitive information such as passwords, these configurations should be deployed using secrets.

### Vault

As we have chosen Vault as our method for storing secrets, a new entry needs to be created in the 'kv' collection. The secret should contain the following parameters:

```
ldap.bindPassword=<BIND_PASSWORD>
ldap.bindDn=<BIND_DN>
ldap.url=<LDAP_URL>
ldap.authentication=simple
ldap.user.baseDn=<LDAP_USER_BASE_DN>
ldap.user.request=(&(objectClass=Person)(sAMAccountName={0}))
ldap.user.realNameAttribute=givenName
ldap.user.emailAttribute=mail
ldap.group.baseDn=<LDAP_GROUP_BASE_DN>
ldap.group.request=(&(cn={0})(objectclass=group))
ldap.group.idAttribute=memberOf
```

The `BIND_PASSWORD`, `BIND_DN`, `LDAP_URL`, `LDAP_USER_BASE_DN`, and `LDAP_GROUP_BASE_DN` parameters need to be set according to your specific configurations.
**Note**: Depending on your setup, adjustments to other parameters may be necessary. The provided configurations are a basic example.

![sonar-secret](https://user-cube.github.io/devops-cheatsheet/assets/images/sonarqube/sonar-secret.png)

### Create External Secret

An external secret must be created to utilize the secret stored in Vault. You can create the external secret as follows (`sonarqube-properties.yaml`):

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: sonar-properties
  namespace: sonarqube
spec:
  data:
  - remoteRef:
      conversionStrategy: Default
      key: kv/sonarqube/properties
      property: sonar-secret
    secretKey: secret.properties
  refreshInterval: 3600s
  secretStoreRef:
    kind: ClusterSecretStore
    name: vault-backend
  target:
    creationPolicy: Owner
    deletionPolicy: Retain
    name: sonar-properties
```

Apply this to the cluster as follows:

```bash
kubectl apply -f sonarqube-properties.yaml
```

The deployed external secret should resemble the following:

```bash
kubectl get externalsecrets -n sonarqube
 
NAME                                                   AGE
clustersecretstore.external-secrets.io/vault-backend   168d
 
NAME                                                  STORE           REFRESH INTERVAL   STATUS
externalsecret.external-secrets.io/sonar-properties   vault-backend   3600s             SecretSynced
```

### Update Sonarqube Helm

With everything in place, the Sonarqube helm needs to be updated. Locate the content in the values file and update it as follows:

```yaml
   sonar.forceAuthentication: true
   sonar.security.realm: LDAP
   # all other sonar.properties are inside the sonarSecretProperties and can be edited in vault
   
# Additional sonar properties to load from a secret with a key "secret.properties" (must be a string)
# sonarSecretProperties:
sonarSecretProperties: sonar-properties
```

This content should be around line ~350.

Now, simply upgrade the Sonarqube helm:

```bash
helm upgrade sonarqube -n sonarqube -f values/sonarqube-values.yaml sonarqube/sonarqube --version 4.0.0+315
```