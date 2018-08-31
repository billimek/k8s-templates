# unifi

## install mysql for recorder component

```shell
helm install --name hass-mysql stable/mysql --values mysql-values.yaml --set mysqlPassword="${HASS_DB_PASSWORD}"
```

## installing

```shell
helm install --name hass billimek/home-assistant --values values.yaml --set ingress.hosts="{hass.$DOMAIN}",extraEnv.CAMERA_AUTH="$CAMERA_AUTH",configurator.ingress.hosts="{config.hass.$DOMAIN}",configurator.username="$HASS_CONFIG_USERNAME",configurator.password="$HASS_CONFIG_PASSWORD",configurator.hassApiPassword="$HASS_API_PASSWORD"
```
