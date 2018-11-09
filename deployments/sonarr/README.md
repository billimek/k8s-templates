# sonarr tv show downloader

## installing / upgrading

```shell
helm upgrade --install sonarr billimek/sonarr --reset-values --values values.yaml --set ingress.hosts="{sonarr.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
