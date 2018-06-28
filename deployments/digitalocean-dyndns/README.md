## digitalocean-dyndns

Based on this [custom helm chart](https://github.com/billimek/billimek-charts/tree/master/uptimerobot)

### install

```bash
helm install --name digitalocean-dyndns billimek/digitalocean-dyndns --values values.yaml --set digitialocean.token="$DO_AUTH_TOKEN",digitialocean.domain="$DOMAIN"
```
