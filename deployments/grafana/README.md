# grafana

![](https://i.imgur.com/hTo49Uo.png)

## installing

```shell
helm install --name grafana stable/grafana --values values.yaml --set ingress.hosts="{grafana.$DOMAIN}",adminPassword="$GRAFANA_PASSWORD"
```

## upgrading

```shell
helm upgrade grafana stable/grafana --values values.yaml --set ingress.hosts="{grafana.$DOMAIN}",adminPassword="$GRAFANA_PASSWORD"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
