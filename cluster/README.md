## HA cluster setup with rancher/rke

![](https://i.imgur.com/Qd7f8lx.png)

### VMs

Built-out the following cluster:

* On `proxmox` (physical device running proxmox)
  * master node `rke-a`
    * 8 CPU
    * 13GB memory
    * `/dev/sda` 196GB thin-provisioned drive for OS
    * ubuntu 16.04
* On `proxmox-b` (physical device running proxmox)
  * master node `rke-b`
    * 4 CPU
    * 13GB memory
    * `/dev/sda` 196GB thin-provisioned drive for OS
    * ubuntu 16.04
* On `proxmox-c` (physical device running proxmox)
  * master node `rke-c`
    * 8 CPU
    * 32GB memory
    * `/dev/sda` 196GB thin-provisioned drive for OS
    * ubuntu 16.04

### kubernetes cluster orchestration

Using rancher, followed [this guide](https://rancher.com/docs/rancher/v2.x/en/installation/ha/)

## rke installation

```shell
rke up --config ./rancher-cluster.yml

export KUBECONFIG=$(pwd)/kube_config_rancher-cluster.yml

kubectl -n kube-system create serviceaccount tiller
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller

helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
helm install stable/cert-manager --name cert-manager --namespace kube-system
helm install rancher-stable/rancher --name rancher --namespace cattle-system --set hostname=r.$DOMAIN --set ingress.tls.source=letsEncrypt --set letsEncrypt.email=$EMAIL
```
