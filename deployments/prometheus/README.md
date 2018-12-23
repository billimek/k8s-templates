# prometheus

![](https://i.imgur.com/xFOepF3.png)

## installing

```shell
helm upgrade --install prom stable/prometheus --values values.yaml --set alertmanager.ingress.hosts="{alert.prom.$DOMAIN}",server.ingress.hosts="{prom.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
