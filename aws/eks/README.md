# EKS

#### List EKS Clusters

```
aws eks list-clusters # default region unless --region= flag used
```

#### Set Proper kubeconfig

```
aws eks update-kubeconfig --name my-cluster
```

#### Get Node info

```
kubectl get nodes
```
