# rook for persistent storage

https://rook.io/

**NOT USING THIS AT THE MOMENT**

## Preparing the proxmox host for OSDs

### Identify the drives

Identify the drive(s) that will be used for OSDs (and metadata) on each host.  In my case,

* proxmox
  * OSD: /dev/sdd (250GB SSD)
* proxmox-b
  * OSD: /dev/sda (500GB SSD)
* proxmox-c
  * OSD: /dev/sda (500GB SSD)

Identify the `/dev/disk/by-id` path for each of the above drives

### Prepare the drives

* For entire drives (e.g. `/dev/sdd`): `sgdisk -Z /dev/<drive>` to completely wipe the drive alltogether.  I do not know if this will cause bad things to run on a partition of a drive, so have not tried

### Add the drives to the VMs

For example, on `proxmox`:

```shell
qm set 106 -scsi1 /dev/disk/by-id/wwn-0x5002538d41df6786
```

* **scsi1** should translate to `/dev/sdb` in the VM

## Install Rook

### Install the rook ceph operator helm chart

Using the 'beta' chart repo for better stability.

When using rancher, it is necessary to set the `agent.flexVolumeDirPath` due to [this](https://github.com/rook/rook/blob/master/Documentation/flexvolume.md#configuring-the-flexvolume-path)

```shell
helm repo add rook-beta https://charts.rook.io/beta
helm search rook-ceph
helm install --name rook-ceph --namespace rook-ceph-system rook-beta/rook-ceph --set agent.flexVolumeDirPath="/var/lib/kubelet/volumeplugins"
```

### Install the rook ceph cluster

```shell
kubectl create -f cluster.yaml
```

After cluster is running, access the dashboard at http://localhost:8001/api/v1/namespaces/rook-ceph/services/http:rook-ceph-mgr-dashboard:7000/proxy/# (assuming `kubectl proxy` is running).  See https://rook.io/docs/rook/v0.8/ceph-dashboard.html

### Create a rook block storage

```shell
kubectl create -f storageclass.yaml
```

### Make this block storageclass the default for the kubernetes cluster

```shell
❯ kubectl get storageclass
NAME              PROVISIONER          AGE
rook-ceph-block   ceph.rook.io/block   7h

❯ kubectl patch storageclass rook-ceph-block -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
storageclass.storage.k8s.io/rook-ceph-block patched
```

## External access (traefik)

After traefik is set-up, run

```shell
kubectl create secret generic traefik-basic-auth-jeff --from-file ../../secrets/auth --namespace rook-ceph
kapply dashboard-ingress.yaml
```

## Rook Toolbox

See [documentation](https://rook.io/docs/rook/v0.8/toolbox.html) for some more details.

### Install the Toolbox pod

```shell
kubectl create -f toolbox.yaml
kubectl -n rook-ceph exec -it rook-ceph-tools bash
```

### Example using the toolbox pod to directly access some of the data from a mysql deployment

```shell
[root@rook-ceph-tools /]# rbd showmapped
id pool        image                                    snap device
0  replicapool pvc-c24a2acd-aa6f-11e8-b27a-02060ff16d88 -    /dev/rbd0
1  replicapool pvc-fcfe66a6-aad9-11e8-8852-56b1aca8038f -    /dev/rbd1
[root@rook-ceph-tools /]# mkdir /tmp/rook-volume
[root@rook-ceph-tools /]# mount /dev/rbd1 /tmp/rook-volume
[root@rook-ceph-tools /]# ls -al /tmp/rook-volume/
total 110632
drwxr-xr-x 6 gluster input     4096 Aug 28 15:50 .
drwxrwxrwt 8 root    root      4096 Aug 28 18:29 ..
-rw-rw---- 1 gluster input       56 Aug 28 15:50 auto.cnf
-rw-rw---- 1 gluster input 50331648 Aug 28 15:50 ib_logfile0
-rw-rw---- 1 gluster input 50331648 Aug 28 15:50 ib_logfile1
-rw-rw---- 1 gluster input 12582912 Aug 28 15:50 ibdata1
drwx------ 2 gluster input    16384 Aug 28 15:49 lost+found
drwx------ 2 gluster input     4096 Aug 28 15:50 mysql
drwx------ 2 gluster input     4096 Aug 28 15:50 performance_schema
drwx------ 2 gluster input     4096 Aug 28 15:50 wordpress
```

## migrate data from filesystem to pvc used by a pod backed by rook-block-storage

1. Make note of the pvc used by the target deployment, `k get persistentvolumeclaims`
1. Scale-down the deployment to 0 replicas to ensure that nothing is accessing the data
1. Log into the toolbox via `kubectl -n rook-ceph exec -it rook-ceph-tools bash`
1. map and mount the pvc inside the rook toolbox:
```
[root@k8s-ha-c /]# rbd map replicapool/pvc-29ae49b2-cbbf-11e8-91c6-ce4d43fc4e66
/dev/rbd3
[root@k8s-ha-c /]# mkdir /tmp/rbd3
[root@k8s-ha-c /]# mount /dev/rbd3 /tmp/rbd3/
[root@k8s-ha-c /]# ls -al /tmp/rbd3/
total 52
drwxr-xr-x 4 root root  4096 Oct  9 12:34 .
drwxrwxrwt 8 root root  4096 Oct  9 12:42 ..
-rw------- 1 root root 32768 Oct  9 12:31 chronograf-v1.db
drwx------ 2 root root 16384 Oct  9 12:30 lost+found
```
1. copy the data to this mounted path in the toolbox:
```
kubectl -n rook-ceph cp archived-default-chronograf-chronograf-pvc-9275a3f0-c018-11e8-91c6-ce4d43fc4e66 rook-ceph-tools:/tmp/rbd3/
```
1. in the toolbox, unmount and unmap the pvc:
```
[root@k8s-ha-c /]# cd
[root@k8s-ha-c ~]# umount /tmp/rbd3/
[root@k8s-ha-c ~]# rbd unmap /dev/rbd3
```
1. scale the deployment back to the original level
