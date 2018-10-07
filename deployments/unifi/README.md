# unifi

## installing

```shell
helm install --name unifi stable/unifi --values values.yaml --set ingress.hosts="{unifi.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
