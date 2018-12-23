# deluge torrent client

![](https://i.imgur.com/HE3Ab40.png)

## installing

```shell
helm upgrade --install deluge billimek/deluge --reset-values --values values.yaml --set ingress.hosts="{deluge.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
