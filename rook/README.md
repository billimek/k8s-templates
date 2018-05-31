helm install --namespace rook-ceph-system -n rook-ceph rook-master/rook-ceph --version v0.7.0-160.g3060813
kubectl create -f rook_cluster.yaml
kubectl create -f storageclass.yaml