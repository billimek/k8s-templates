# influxdb

## install

```shell
helm install --name influxdb stable/influxdb --values values.yaml --set user.password="$INFLUXDB_PASSWORD"
```

## upgrade

```shell
helm upgrade influxdb stable/influxdb --reset-values --values values.yaml --set user.password="$INFLUXDB_PASSWORD"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
```
