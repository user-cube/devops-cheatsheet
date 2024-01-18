---
title: Kubernetes DNS Debug
layout: home
nav_order: 2
grand_parent: Kubernetes
parent: Kubernetes DNS
has_children: true
permalink: docs/kubernetes/dns/debug
last_modified_date: 2024-01-18
---

# DNS Debugging

Debugging DNS issues in Kubernetes can be a complex task due to the distributed nature of the system. Here are some common steps you might take:

1. **Check the DNS Service**: Ensure that the DNS service is running correctly in your cluster. You can use the `kubectl get services` command to check the status of the service.

2. **Check DNS Endpoints**: Use the `kubectl get endpoints kube-dns --namespace=kube-system` command to check the endpoints of the DNS service.

3. **Check DNS Pods**: Ensure that the DNS pods are running correctly. You can use the `kubectl get pods --namespace=kube-system` command to check the status of the pods.

4. **Check DNS Configuration**: Check the configuration of your DNS service. The configuration file is typically located at `/etc/resolv.conf` on each of your nodes.

5. **Test DNS Resolution**: You can test DNS resolution within your cluster by creating a simple pod and using the `nslookup` command to query the DNS service.

6. **Check Network Policies**: If you're using network policies, ensure that they're not blocking DNS traffic.

7. **Check Logs**: Check the logs of your DNS pods for any error messages or warnings. You can use the `kubectl logs` command to view the logs.

Remember, these are just general steps and the exact debugging process can vary depending on your specific setup and the nature of the issue.

## DNS Utils

DNS Utils is a useful tool in Kubernetes for debugging DNS related issues. It's essentially a prepackaged set of tools installed in a pod that you can use to investigate DNS problems.

To use DNS Utils in Kubernetes, you can create a pod that uses the `dnsutils` image. This image includes a variety of tools such as `dig`, `nslookup`, and `host` that can be used to probe and investigate DNS issues.

Here's an example of how you can create a DNS Utils pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dnsutils
  namespace: default
spec:
  containers:
  - name: dnsutils
    image: k8s.gcr.io/e2e-test-images/jessie-dnsutils:1.3
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
  restartPolicy: Always
```

Execute the following command:

```bash
kubectl apply -f dnsutils.yaml

kubectl get pods dnsutils
NAME      READY     STATUS    RESTARTS   AGE
dnsutils   1/1       Running   0          <some-time>
```

Once that Pod is running, you can exec nslookup in that environment. If you see something like the following, DNS is working correctly.

```bash
kubectl exec -i -t dnsutils -- nslookup kubernetes.default
Server:    10.0.0.10
Address 1: 10.0.0.10
 
Name:      kubernetes.default
Address 1: 10.0.0.1
```

To read more about this debugging pod please follow the official [Kubernetes documentation](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/).