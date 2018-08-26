## metrics-server

From [this chart](https://github.com/kubernetes/charts/tree/master/stable/metrics-server):

This is supposed to replace heapster - not sure how it comes into play with the kubernetes dashboard and the metrics related to that.  There is an [issue](https://github.com/kubernetes/dashboard/issues/2986) to integrate metrics-server with dashboard.

### installing

```shell
helm install --name metrics-server --namespace kube-system stable/metrics-server --values values.yaml
```