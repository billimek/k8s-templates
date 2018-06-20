## grafana


### installing

```bash
helm install --name grafana stable/grafana --values values.yaml --set ingress.hosts="{grafana.$DOMAIN}",adminPassword="$GRAFANA_PASSWORD"
```

### upgrading

```bash
### upgrading

```bash
helm upgrade grafana stable/grafana --values values.yaml --set ingress.hosts="{grafana.$DOMAIN}",adminPassword="$GRAFANA_PASSWORD"
```
