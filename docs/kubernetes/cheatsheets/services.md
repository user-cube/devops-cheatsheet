---
title: Services
layout: home
grand_parent: Kubernetes
parent: Kubernetes Cheat Sheets
nav_order: 2
last_modified_date: 2024-01-18
---

# Services in Kubernetes

A Service in Kubernetes is an abstraction that defines a logical set of Pods and a policy by which to access them. Services enable a loose coupling between dependent Pods. A Service is defined using YAML (preferred) or JSON, like all Kubernetes objects.

## Table of Contents

- [Services in Kubernetes](#services-in-kubernetes)
  * [Table of Contents](#table-of-contents)
  * [Why Use a Service?](#why-use-a-service)
  * [Types of Services](#types-of-services)
  * [Service Discovery](#service-discovery)
  * [Connecting Applications with Services](#connecting-applications-with-services)
  * [Service Lifecycle](#service-lifecycle)
  * [Cheat Sheets](#cheat-sheets)

## Why Use a Service?

Services are crucial when you want to expose your pod to the outside world or within the cluster. They allow your applications to start and replicate as needed. Services will ensure that your application remains available despite individual pod or node failures, providing high availability.

## Types of Services

There are four types of services in Kubernetes:

1. **ClusterIP**: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster.

2. **NodePort**: Exposes the Service on each Node’s IP at a static port (the NodePort). A ClusterIP Service, to which the NodePort Service routes, is automatically created.

3. **LoadBalancer**: Exposes the Service externally using a cloud provider’s load balancer. NodePort and ClusterIP Services, to which the external load balancer routes, are automatically created.

4. **ExternalName**: Maps the Service to the contents of the externalName field (e.g., `foo.bar.example.com`), by returning a CNAME record with its value.

## Service Discovery

Kubernetes supports two primary modes of finding a Service - environment variables and DNS. The former works out of the box while the latter requires the CoreDNS to be running in the cluster.

## Connecting Applications with Services

Services match a set of Pods using labels and selectors, a pattern that decouples the way in which clients handle their dependencies. Services monitor continuously updated endpoints to ensure the traffic is directed to the right pods.

## Service Lifecycle

When you create a Service, it creates a corresponding Endpoints object, listing the IP addresses of the Pods that match the Service selector. If you update the set of Pods, the Endpoints get automatically updated, and the clients will be directed to the new set of Pods.

Remember, Services allow your applications to scale and communicate. They provide discovery and routing functionality for Pods.

![Kubernetes Services](https://user-cube.github.io/devops-cheatsheet/assets/images/kubernetes/services.svg)

## Cheat Sheets

| Name                                                                                   | Command                                                                                                      |
|----------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| List all services                                                                      | `kubectl get services`                                                                                       |
| List all services for all namespaces                                                   | `kubectl get services -A`                                                                                    |
| List all services in ps output format with more information (such as node name)        | `kubectl get services -o wide`                                                                               |
| Get service configurations as yaml                                                     | `kubectl get service <NAME> -o yaml`                                                                         |
| Get service information                                                                | `kubectl describe service/<NAME>`                                                                            |
| List a single service with specified NAME in ps output format                          | `kubectl get service <NAME>`                                                                                 |
| List all services with labels                                                          | `kubectl get services --show-labels`                                                                         |
| List services in JSON output format, in the "v1" version of the "core" API group       | `kubectl get services.v1.core -o json`                                                                       |
| List a single service in JSON output format                                            | `kubectl get -o json service/<NAME>`                                                                         |
| List a service identified by type and name specified in "service.yaml" in JSON format  | `kubectl get -f service.yaml -o json`                                                                        |
| List resources from a directory with kustomization.yaml - e.g. dir/kustomization.yaml  | `kubectl get -k dir/`                                                                                        |
| Return only the clusterIP value of the specified service                               | `kubectl get -o template service/<NAME> {% raw %}--template={{.spec.clusterIP}} {% endraw %}`                |
| List service information in custom columns                                             | `kubectl get service NAME -o custom-columns=TYPE:.spec.type,CLUSTER-IP:.spec.clusterIP`                      |
| List all replication controllers, services and pods together in ps output format       | `kubectl get rc,services,pods`                                                                               |
| List one or more resources by their type and names                                     | `kubectl get rc/<NAME> service/<NAME> pods/<NAME>`                                                           |
| Forward one or more local ports to a service                                           | `kubectl port-forward service/<NAME> <LOCAL_PORT>:<SERVICE_PORT>`                                            |