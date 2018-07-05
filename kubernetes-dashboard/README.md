## kubernetes dashboard for GUI stuff

From [this guide](https://joshrendek.com/2018/04/kubernetes-on-bare-metal/):

## Installing

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
kubectl apply -f dashboard-user.yaml
```

Set session to never expire by editing the configuration and adding the following as a runtime argument: `"--token-ttl=0"`

Grab the token via `kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d '\t'`

After traefik was set-up, ran 

```
kubectl apply -f dashboard-ingress.yaml
```


## (Alternative - helm chart) - did not use this

```
helm install --namespace kube-system --name kubernetes-dashboard stable/kubernetes-dashboard --values values.yaml --set ingress.hosts="{d.k.$DOMAIN}"
```