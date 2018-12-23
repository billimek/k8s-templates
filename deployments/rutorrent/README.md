# rutorrent torrent client

## installing

```shell
helm upgrade --install rutorrent billimek/rutorrent --reset-values --values values.yaml --set ingress.hosts="{rutorrent.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
