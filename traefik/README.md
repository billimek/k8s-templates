## traefik 

* Want to use traefik as a [HA cluster](https://docs.traefik.io/user-guide/cluster/)
* There is an [open PR](https://github.com/kubernetes/charts/pull/5563) to support consul in traefik for the official helm chart.
* Cloned this repo https://github.com/medialaan/k8s-charts-kubernetes.git and ran the following commands inside `stable/traefik`:

```
helm repo index .
helm serve . &
helm install --name traefik --namespace kube-system --values ~/traefik_values.yaml local/traefik
```

Regarding [traefik_values.yaml](traefik_values.yaml): Hard-coded the nodePorts so I don't need to keep changing haproxy's config.