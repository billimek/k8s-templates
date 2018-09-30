# rook for persistent storage

https://rook.io/

## Preparing the proxmox host for OSDs

### Identify the drives

Identify the drive(s) that will be used for OSDs (and metadata) on each host.  In my case,

* proxmox
  * OSD: /dev/sdd (250GB SSD)
  * Metadata/Journal: /dev/nvme0n1p4 (10GB NVMe SSD)
* proxmox-b
  * OSD: /dev/sda (500GB SSD)
  * Metadata/Journal: /dev/nvme0n1p4 (10GB NVMe SSD)
* proxmox-c
  * OSD: /dev/sda (500GB SSD)
  * Metadata/Journal: /dev/nvme0n1p4 (10GB NVMe SSD)

Identify the `/dev/disk/by-id` path for each of the above drives

### Prepare the drives

* For entire drives (e.g. `/dev/sdd`): `sgdisk -Z /dev/<drive>` to completely wipe the drive alltogether.  I do not know if this will cause bad things to run on a partition of a drive, so have not tried
* For partitions (e.g. `/dev/nvme0n1p4`): I use `parted` to delete and re-create the partition - not sure the appropriate path to take for a partition

### Add the drives to the VMs

For example, on `proxmox`:

```shell
qm set 106 -scsi1 /dev/disk/by-id/wwn-0x5002538d41df6786
qm set 106 -scsi2 /dev/disk/by-id/nvme-Samsung_SSD_960_EVO_500GB_S3X4NB0K206387N-part4
```

* **scsi1** should translate to `/dev/sdb` in the VM
* **scsi2** should translate to `/dev/sdc` in the VM

## Install Rook

### Install the rook ceph operator helm chart

(the version will change - also consider installing alpha or beta instead for more stability?)

```shell
helm repo add rook-master https://charts.rook.io/master
helm search rook-ceph
helm install --name rook-ceph --namespace rook-ceph-system rook-master/rook-ceph --version v0.8.0-125.g2bcfb32
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
