## chronograf

```bash
helm install --name chronograf stable/chronograf --values values.yaml --set ingress.hostname="chronograf.$DOMAIN"
```
