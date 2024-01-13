---
title: Sonarqube
layout: home
nav_order: 6
permalink: docs/sonarqube
last_modified_date: 2024-01-13
---

# Sonarqube

SonarQube is an open-source platform for continuous inspection of code quality. It provides static code analysis to detect bugs, code smells, and security vulnerabilities in various programming languages. SonarQube integrates with build systems and code repositories to automatically analyze code quality as part of the development process.

SonarQube supports a wide range of programming languages and offers detailed reports on code quality metrics, such as code duplication, complexity, and test coverage. It also provides security-focused analysis to identify potential security vulnerabilities in the codebase.

Developers and teams use SonarQube to maintain and improve the quality of their code, ensuring that it meets industry standards and best practices. By integrating SonarQube into the development workflow, teams can proactively identify and address code quality issues, leading to more reliable and secure software.


![sonarqube](https://user-cube.github.io/devops-cheatsheet/assets/images/sonarqube/sonarqube-logo.png)

## Table of Contents

- [Sonarqube](#sonarqube)
  * [Table of Contents](#table-of-contents)
  * [LDAP Integration](#ldap-integration)
    + [Vault](#vault)
    + [Create external secret](#create-external-secret)
    + [Update sonarqube helm](#update-sonarqube-helm)

## LDAP Integration

In order to integrate SonarQube with LDAP we need to define a couple parameters on sonar. This parameters can be set directly on the helm or being used in secrets. Since LDAP contains sensitive information like passwords we are going to deploy this configurations using secrets.

### Vault

Since we defined that vault is our way of storing secrets, we need to create a new entry (for this case we defined a collection called `kv`). Our secret should contain the following parameters:

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

You will need to set `BIND_PASSWORD`, `BIND_DN`, `LDAP_URL`, `LDAP_USER_BASE_DN` and `LDAP_GROUP_BASE_DN` to your own configurations.
**Note**: Depending on your configuration you might need to adjust other parameters, this is just an example of basic configurations.

![sonar-secret](https://user-cube.github.io/devops-cheatsheet/assets/images/sonarqube/sonar-secret.png)

### Create external secret

Now we need to create an external secret in order to use this secret stored on vault. You can create the external secret as follows (`sonarqube-properties.yaml`):

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

Now you need to apply this on the cluster:

```bash
kubectl apply -f sonarqube-properties.yaml
```

The externalsecret deployed should look like this:

```bash
kubectl get externalsecrets -n sonarqube
 
NAME                                                   AGE
clustersecretstore.external-secrets.io/vault-backend   168d
 
NAME                                                  STORE           REFRESH INTERVAL   STATUS
externalsecret.external-secrets.io/sonar-properties   vault-backend   3600s              SecretSynced
```

### Update sonarqube helm

Now that everything is in place you need to update the helm. Look for this content in the values file and update it like this:

```yaml
   sonar.forceAuthentication: true
   sonar.security.realm: LDAP
   # all other sonar.properties are inside the sonarSecretProperties and can be edited in vault
   
# Additional sonar properties to load from a secret with a key "secret.properties" (must be a string)
# sonarSecretProperties:
sonarSecretProperties: sonar-properties
```

This content should be on line ~350 line.

Now you only need to upgrade the sonarqube helm:

```bash
helm upgrade sonarqube -n sonarqube -f values/sonarqube-values.yaml sonarqube/sonarqube --version 4.0.0+315
```