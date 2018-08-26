## kubernetes dashboard for GUI stuff

From [this guide](https://joshrendek.com/2018/04/kubernetes-on-bare-metal/):

### Installing

```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
kubectl apply -f dashboard-user.yaml
```

### Accessing the dashboard

Set session to never expire by editing the configuration and adding the following as a runtime argument: `"--token-ttl=0"` in the containers section,

```yaml
        "containers": [
          {
            "name": "kubernetes-dashboard",
            "image": "k8s.gcr.io/kubernetes-dashboard-amd64:v1.8.3",
            "args": [
              "--auto-generate-certificates",
              "--token-ttl=0"
            ],
```

Grab the token via `kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d '\t'`

### External access (traefik)

After traefik was set-up, ran 

```shell
kubectl apply -f dashboard-ingress.yaml
```

### Heapster/metrics

kubernetes dashboard doesn't seem to support heapster any more for metrics, because heapster is being deprecated in favor of [**metrics-server**](https://github.com/kubernetes-incubator/metrics-server).  Unfortunatley [kubernetes dashboard doesn't yet support metrics-server](https://github.com/kubernetes/dashboard/issues/2986), so no metrics are possible in dashboard at this time, as far as I can tell.