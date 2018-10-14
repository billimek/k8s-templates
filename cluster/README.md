## HA cluster setup with kubeadm

### VMs

Built-out the following cluster:

* On `proxmox` (physical device running proxmox)
  * master node `k8s-ha-a`
    * 8 CPU
    * 16GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 232.9G thin-provisioned drive for ceph OSD
    * ubuntu 16.04
* On `proxmox-b` (physical device running proxmox)
  * master node `k8s-ha-b`
    * 4 CPU
    * 6GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 465.8GB thin-provisioned drive for ceph OSD
    * ubuntu 16.04
* On `proxmox-c` (physical device running proxmox)
  * master node `k8s-ha-b`
    * 8 CPU
    * 32GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * `/dev/sdb` 465.8GB thin-provisioned drive for ceph OSD
    * ubuntu 16.04

### kubernetes cluster orchestration

Using rancher, followed [this guide](https://rancher.com/docs/rancher/v2.x/en/installation/ha/)