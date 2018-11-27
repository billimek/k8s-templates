# Plex Media Server

![](https://i.imgur.com/nDyS9OA.jpg)


## installing

```shell
helm install --name plex billimek/kube-plex --values values.yaml --set ingress.hosts="{plex.$DOMAIN}",claimToken="$PLEX_CLAIM_TOKEN"
```

## upgrading

```shell
helm upgrade plex billimek/kube-plex --reset-values --values values.yaml --set ingress.hosts="{plex.$DOMAIN}",claimToken="$PLEX_CLAIM_TOKEN"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
