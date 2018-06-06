## kubernetes dashboard for GUI stuff

From [this guide](https://joshrendek.com/2018/04/kubernetes-on-bare-metal/):

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
kubectl apply -f dashboard-user.yaml
```

Grab the token via `kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d '\t'`

After traefik was set-up, ran 

```
kubectl apply -f dashboard_ingress.yaml
```