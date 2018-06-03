## HA cluster setup with kubeadm

Built-out the following cluster:

* On `proxmox` (physical device running proxmox)
  * master node `k8s`
    * 4 CPU
    * 4GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * NFS-mounted `/mnt/rook` from zfs `/tank/rook` carved-out volume on `proxmox` for rook to use
    * ubuntu 18.04
    * will 'float' between `proxmox` and `proxmox-b` as needed for capacity and downtime - set-up in proxmox as a HA VM to run on either proxmox node as well as storage replication between the two for very fast live-migration when needed
  * master node `k8s-c`
    * 4 CPU
    * 4GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 100GB thin-provisioned drive for rook to use
    * ubuntu 18.04
    * will stay locked to proxmox-b
* On `proxmox-b` (physical device running proxmox)
  * master node `k8s-b`
    * 4 CPU
    * 4GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 100GB thin-provisioned drive for rook to use
    * ubuntu 18.04
    * will stay locked to proxmox and is also the node where the large NAS array is held by `proxmox`. will consider running workloads that need access to the NAS array only on this node


Mostly followed the following two guides:

* https://joshrendek.com/2018/04/kubernetes-on-bare-metal/
* https://kubernetes.io/docs/setup/independent/high-availability/