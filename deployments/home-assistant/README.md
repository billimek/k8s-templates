## unifi

### installing

```bash
helm install --name hass billimek/home-assistant --values values.yaml --set ingress.hosts="{hass.$DOMAIN}",extraEnv.CAMERA_AUTH="$CAMERA_AUTH",configurator.ingress.hosts="{config.hass.$DOMAIN}",configurator.username="$HASS_CONFIG_USERNAME",configurator.password="$HASS_CONFIG_PASSWORD",configurator.hassApiPassword="$HASS_API_PASSWORD"
```

### install mariaDB for recorder component

```bash
helm install --name hass-maraidb stable/mariadb --values mariadb-values.yaml --set db.password="${HASS_DB_PASSWORD}"

```