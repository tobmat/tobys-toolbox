---
description: K8 info
---

# Kubernetes

Status a pod in specific namespace

```
kubectl --kubeconfig /tmp/eks.test get all -n azure-devops
```

Display where image(s) are pulled from

```
kubectl --kubeconfig /tmp/eks.test get pods -n azure-devops -o jsonpath="{..image}" |tr -s '[[:space:]]' '\n' |sort |uniq -c
   2 harbor.paas.karops.io/infrastructure/adoagent:73526
```

List all resources

```
kubectl api-resources --verbs=list --namespaced -o name   | xargs -n 1 kubectl get --show-kind --ignore-not-found  -n svc-accts
```
