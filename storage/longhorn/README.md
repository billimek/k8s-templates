# longhorn for replicated persistent storage

https://github.com/rancher/longhorn

**NOT USING THIS AT THE MOMENT**

## Install Longhorn

Installed via the rancher 'catalog' UI.  Used the following settings:

* Longhorn Kubernetes Driver: *csi*
* Default Storage Class: *False*
* Exposde app using Layer 7 Load Balancer: *False*
* Longhorn UI Service: *ClusterIP*

### Setting-up traefik ingress for longhorn UI

```shell
k create secret generic traefik-basic-auth-jeff --from-file ../../secrets/auth --namespace longhorn-system
kapply longhorn-ingress.yaml
```

## Installing via Helm

There may be a better way to install longhorn via a helm chart, but at this time it isn't understood how to do this.
