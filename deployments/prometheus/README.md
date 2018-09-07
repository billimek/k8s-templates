# prometheus

## installing

```shell
helm install stable/prometheus --name prom --values values.yaml --set alertmanager.ingress.hosts="{alert.prom.$DOMAIN}",server.ingress.hosts="{prom.$DOMAIN}"
```

## upgrading

```shell
helm upgrade prom stable/prometheus --values values.yaml --set alertmanager.ingress.hosts="{alert.prom.$DOMAIN}",server.ingress.hosts="{prom.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```