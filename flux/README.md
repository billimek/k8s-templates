# WeaveWorks Flux

https://github.com/weaveworks/flux

## Installation

```shell
helm upgrade --install flux --set rbac.create=true --set helmOperator.create=true --set helmOperator.updateChartDeps=false --set git.url=git@github.com:billimek/k8s-gitops --namespace flux weaveworks/flux
```

## Usage

See [k8s-gitops](https://github.com/billimek/k8s-gitops) repo for implementation