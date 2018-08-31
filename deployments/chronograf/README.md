# chronograf

## installing

```shell
helm install --name chronograf stable/chronograf --values values.yaml --set ingress.hostname="chronograf.$DOMAIN"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```