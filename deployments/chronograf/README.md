# chronograf

![](https://i.imgur.com/PPbhf5O.png)

## installing

```shell
helm upgrade --install chronograf stable/chronograf --reset-values --values values.yaml --set ingress.hostname="chronograf.$DOMAIN"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
