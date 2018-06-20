## prometheus


### installing

```bash
helm install stable/prometheus --name prom --values values.yaml --set alertmanager.ingress.hosts="{alert.prom.$DOMAIN}",server.ingress.hosts="{prom.$DOMAIN}"
```

### upgrading

```bash
helm upgrade prom stable/prometheus --values values.yaml --set alertmanager.ingress.hosts="{alert.prom.$DOMAIN}",server.ingress.hosts="{prom.$DOMAIN}"
```