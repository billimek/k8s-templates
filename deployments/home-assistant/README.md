## unifi

### installing

```bash
helm install --name hass billimek/home-assistant --values values.yaml --set ingress.hosts="{hass.$DOMAIN}",extraEnv.CAMERA_AUTH="$CAMERA_AUTH",configurator.ingress.hosts="{hass-config.$DOMAIN}",configurator.credentials="$HASS_CONFIG_CREDENTIALS",configurator.hassApiPassword="$HASS_API_PASSWORD"
```

### install mariaDB for recorder component

```bash
helm install --name hass-maraidb stable/mariadb --values mariadb-values.yaml --set db.password="${HASS_DB_PASSWORD}"

```