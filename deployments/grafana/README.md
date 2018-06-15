## chronograf

```bash
helm install --name grafana stable/grafana --values values.yaml --set ingress.hosts="{grafana.$DOMAIN}",adminPassword="$GRAFANA_PASSWORD"
```
