# unifi

## installing

```shell
helm install --name unifi billimek/unifi --values values.yaml --set ingress.hosts="{unifi.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
