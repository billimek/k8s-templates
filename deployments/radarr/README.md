# radarr movie downloader

## installing

```shell
helm install --name radarr billimek/radarr --values values.yaml --set ingress.hosts="{radarr.$DOMAIN}"
```

## upgrading

```shell
helm upgrade radarr billimek/radarr --reset-values --values values.yaml --set ingress.hosts="{radarr.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
