## influxdb

```bash
helm install --name influxdb stable/influxdb --values values.yaml --set user.password="$INFLUXDB_PASSWORD"
```