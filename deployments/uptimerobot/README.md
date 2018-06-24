## uptimerobot

Based on this [custom helm chart](https://github.com/billimek/billimek-charts/tree/master/uptimerobot)

### install

```bash
helm install --name uptimerobot billimek/uptimerobot --values values.yaml --set config.uptimerobot.apikey="$UPTIMEROBOT_APIKEY"
```
