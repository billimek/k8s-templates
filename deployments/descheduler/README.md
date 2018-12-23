# desheduler

* https://github.com/kubernetes-incubator/descheduler
* https://akomljen.com/meet-a-kubernetes-descheduler/


## installing

```shell
helm upgrade --install ds akomljen-charts/descheduler --namespace kube-system --reset-values --values values.yaml
```
