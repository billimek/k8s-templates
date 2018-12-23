# Plex Media Server

## installing

```shell
helm upgrade --install plex billimek/kube-plex --reset-values --values values.yaml --set ingress.hosts="{plex.$DOMAIN}",claimToken="$PLEX_CLAIM_TOKEN"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
