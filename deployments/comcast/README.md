## comcast

![](https://i.imgur.com/mSBIWuu.png)

Based on this [custom helm chart](https://github.com/billimek/billimek-charts/tree/master/comcast)

### install

```bash
helm install --name comcast billimek/comcast --values values.yaml --set config.comcast.username="$COMCAST_USERNAME",config.comcast.password="$COMCAST_PASSWORD"
```
