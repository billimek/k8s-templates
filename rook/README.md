## rook cluster for storage 

Followed [this guide](https://rook.io/docs/rook/master/quickstart.html)

```
helm repo add rook-master https://charts.rook.io/master
helm search rook-ceph
helm install --namespace rook-ceph-system -n rook-ceph rook-master/rook-ceph --version v0.7.0-160.g3060813
kubectl create -f rook_cluster.yaml
kubectl create -f storageclass.yaml
```