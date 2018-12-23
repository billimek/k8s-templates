# radarr movie downloader

![](https://i.imgur.com/eAgWySC.png)


## installing / upgrading

```shell
helm upgrade --install radarr billimek/radarr --reset-values --values values.yaml --set ingress.hosts="{radarr.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
