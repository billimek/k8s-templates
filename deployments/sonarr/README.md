# sonarr tv show downloader

## installing

```shell
helm install --name sonarr billimek/sonarr --values values.yaml --set ingress.hosts="{sonarr.$DOMAIN}"
```

## upgrading

```shell
helm upgrade sonarr billimek/sonarr --reset-values --values values.yaml --set ingress.hosts="{sonarr.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
