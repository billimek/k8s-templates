## metrics-server

From [this chart](https://github.com/kubernetes/charts/tree/master/stable/metrics-server):

This is supposed to replace heapster - not sure how it comes into play with the kubernetes dashboard and the metrics related to that.

```
helm install stable/metrics-server --namespace kube-system --name metrics-server --values values.yaml
```