# sonarr tv show downloader

![](https://i.imgur.com/0CS5ADs.png)

## installing / upgrading

```shell
helm upgrade --install sonarr billimek/sonarr --reset-values --values values.yaml --set ingress.hosts="{sonarr.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
