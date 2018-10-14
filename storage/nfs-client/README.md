## nfs-based dyanmic storage class

Using the [nfs-client storage type](https://github.com/kubernetes-incubator/external-storage/tree/master/nfs-client)

### install

Need to install nfs-client on each node (`apt-get install nfs-client`)

```shell
helm install --name nfs-client-provisioner stable/nfs-client-provisioner --set nfs.server=10.0.10.7 --set nfs.path=/tank/data/k8s-nfs
```

### upgrading

```shell
helm upgrade nfs-client-provisioner stable/nfs-client-provisioner --set nfs.server=10.0.10.7 --set nfs.path=/tank/data/k8s-nfs
```

### testing

Test this with:

```shell
kubectl create -f test-pod.yaml
kubectl create -f test-claim.yaml
```

After the host-NFS mount has a SUCCESS file (e.g.):

```shell
root@k8s:/mnt# ls -al /srv/default-test-claim-pvc-583a0880-6c27-11e8-82ec-363e8457094a/
total 8
drwxrwxrwx 2 root root 4096 Jun  9 20:54 .
drwxr-xr-x 3 root root 4096 Jun  9 20:54 ..
-rw-r--r-- 1 root root    0 Jun  9 20:54 SUCCESS
```

Delete the test thing via:

```shell
kubectl delete -f test-claim.yaml
kubectl delete -f test-pod.yaml
```