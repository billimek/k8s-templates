# home assistant

![](https://i.imgur.com/OMwEZYO.png)

## install mysql for recorder component

```shell
helm install --name hass-mysql stable/mysql --values mysql-values.yaml --set mysqlPassword="${HASS_DB_PASSWORD}"
```

## installing

```shell
helm install --name hass stable/home-assistant --values values.yaml --set ingress.hosts="{hass.$DOMAIN}",extraEnv.CAMERA_AUTH="$CAMERA_AUTH",configurator.ingress.hosts="{config.hass.$DOMAIN}",configurator.username="$HASS_CONFIG_USERNAME",configurator.password="$HASS_CONFIG_PASSWORD",configurator.hassApiPassword="$HASS_API_PASSWORD",configurator.hassApiUrl="https://hass.$DOMAIN/api/"
```

## upgrading

```shell
helm upgrade hass stable/home-assistant --values values.yaml --set ingress.hosts="{hass.$DOMAIN}",extraEnv.CAMERA_AUTH="$CAMERA_AUTH",configurator.ingress.hosts="{config.hass.$DOMAIN}",configurator.username="$HASS_CONFIG_USERNAME",configurator.password="$HASS_CONFIG_PASSWORD",configurator.hassApiPassword="$HASS_API_PASSWORD",configurator.hassApiUrl="https://hass.$DOMAIN/api/"
```

## backup (stash)

```shell
kubectl create -f stash.yaml
kubectl create -f mysql-stash.yaml
```
