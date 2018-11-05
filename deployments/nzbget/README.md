# nzbget usenet client

## installing

```shell
helm install --name nzbget billimek/nzbget --values values.yaml --set ingress.hosts="{nzbget.$DOMAIN}"
```

## upgrading

```shell
helm upgrade nzbget billimek/nzbget --reset-values --values values.yaml --set ingress.hosts="{nzbget.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```