## unifi

### installing

```bash
helm install --name unifi billimek/unifi --values values.yaml --set ingress.hosts="{unifi.$DOMAIN}"
```

