# deluge torrent client

![](https://i.imgur.com/HE3Ab40.png)

## installing

```shell
helm install --name deluge billimek/deluge --values values.yaml --set ingress.hosts="{deluge.$DOMAIN}"
```

## upgrading

```shell
helm upgrade deluge billimek/deluge --reset-values --values values.yaml --set ingress.hosts="{deluge.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
