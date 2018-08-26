## HA cluster setup with kubeadm

Built-out the following cluster:

* On `proxmox` (physical device running proxmox)
  * master node `k8s-ha-a`
    * 8 CPU
    * 16GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 9.4GB thin-provisioned drive for ceph journal/metadata cache
    * `/dev/sdc` 232.9G thin-provisioned drive for ceph OSD
    * ubuntu 16.04
    * will 'float' between `proxmox` and `proxmox-b` as needed for capacity and downtime - set-up in proxmox as a HA VM to run on either proxmox node as well as storage replication between the two for very fast live-migration when needed
* On `proxmox-b` (physical device running proxmox)
  * master node `k8s-ha-b`
    * 4 CPU
    * 6GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 9.4GB thin-provisioned drive for ceph journal/metadata cache
    * `/dev/sdc` 465.8GB thin-provisioned drive for ceph OSD
    * ubuntu 16.04
* On `proxmox-c` (physical device running proxmox)
  * master node `k8s-ha-b`
    * 8 CPU
    * 32GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 9.4GB thin-provisioned drive for ceph journal/metadata cache
    * `/dev/sdc` 465.8GB thin-provisioned drive for ceph OSD
    * ubuntu 16.04

Mostly followed: https://kubernetes.io/docs/setup/independent/high-availability/
