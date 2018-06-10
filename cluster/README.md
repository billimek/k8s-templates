## cluster setup with kubeadm

Built-out the following cluster:

* On `proxmox` (physical device running proxmox)
  * master node `k8s`
    * 4 CPU
    * 4GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * ubuntu 18.04
    * will 'float' between `proxmox` and `proxmox-b` as needed for capacity and downtime - set-up in proxmox as a HA VM to run on either proxmox node as well as storage replication between the two for very fast live-migration when needed
* On `proxmox-b` (physical device running proxmox)
  * master node `k8s-b`
    * 4 CPU
    * 4GB memory
    * `/dev/sda` 32GB thin-provisioned drive for OS
    * ubuntu 18.04

Mostly followed the following two guides:

* https://joshrendek.com/2018/04/kubernetes-on-bare-metal/
* https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/