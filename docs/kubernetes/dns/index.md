---
title: Kubernetes DNS
layout: home
nav_order: 3
parent: Kubernetes
has_children: true
permalink: docs/kubernetes/dns
last_modified_date: 2024-01-18
---

# DNS

DNS, or Domain Name System, is a system used to translate human-friendly domain names, such as `www.example.com`, into the numerical IP addresses required for locating and identifying computer services and devices. This translation is necessary because while computers and other network devices use IP addresses to locate and connect to each other, humans generally find it easier to use and remember domain names.

In the context of Kubernetes, DNS is a built-in service for the discovery of Kubernetes services. When a service is created within Kubernetes, it is automatically assigned a DNS name. This allows other services in the cluster to locate the service using a simple domain name, rather than needing to keep track of specific IP addresses. 

For example, if you have a service named `my-service` in a Kubernetes namespace `my-ns`, the DNS name for the service would be `my-service.my-ns.svc.cluster.local`. Any other service within the same cluster can use this DNS name to connect to the service, without needing to know its IP address. 

If you're having issues with DNS resolution in Kubernetes, it could be due to a variety of reasons such as misconfiguration of DNS services, network issues, or problems with the underlying nodes or pods.