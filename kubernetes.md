---
description: K8 info
---

# Kubernetes

Status a pod in specific namespace

```text
kubectl --kubeconfig /tmp/eks.test get all -n azure-devops
```

Display where image\(s\) are pulled from

```text
kubectl --kubeconfig /tmp/eks.test get pods -n azure-devops -o jsonpath="{..image}" |tr -s '[[:space:]]' '\n' |sort |uniq -c
   2 harbor.paas.karops.io/infrastructure/adoagent:73526
```

