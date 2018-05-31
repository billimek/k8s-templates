## consul

```
helm install --name consul --set StorageClass=rook-ceph-block --namespace kube-system stable/consul
```