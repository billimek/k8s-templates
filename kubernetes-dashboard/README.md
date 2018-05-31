## kubernetes dashboard for GUI stuff

From [this guide](https://joshrendek.com/2018/04/kubernetes-on-bare-metal/):

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
kubectl apply -f dashboard-user.yaml
```

After traefik was set-up, ran 

```
kubectl apply -f dashboard_ingress.yaml
```