## nfs-based dyanmic storage class

Using the [nfs-client storage type](https://github.com/kubernetes-incubator/external-storage/tree/master/nfs-client)

Need to install nfs-client on each node (`apt-get install nfs-client`)

```shell
kubectl apply -f deployment.yaml
kubectl apply -f class.yaml
kubectl create -f https://raw.githubusercontent.com/kubernetes-incubator/external-storage/master/nfs-client/deploy/auth/serviceaccount.yaml
kubectl create -f https://raw.githubusercontent.com/kubernetes-incubator/external-storage/master/nfs-client/deploy/auth/clusterrole.yaml
kubectl create -f https://raw.githubusercontent.com/kubernetes-incubator/external-storage/master/nfs-client/deploy/auth/clusterrolebinding.yaml
```

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