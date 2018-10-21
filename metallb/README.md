# MetalLB

https://metallb.universe.tf/installation/

## installation

This installs MetaLB using the layer2 mode with reserved service IPs being 10.0.7.80-10.0.7.95.

```shell
helm install --name metallb stable/metallb -f values.yaml
```
