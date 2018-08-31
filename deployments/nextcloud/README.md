# nextcloud

## installing

```bash
helm install --name nextcloud billimek/nextcloud --values values.yaml --set ingress.hosts="{nextcloud.$DOMAIN}",nextcloudPassword="$NEXTCLOUD_PASSWORD",nextcloudEmail="$NEXTCLOUD_EMAIL",nextcloudHost="nextcloud.$DOMAIN",mariadb.mariadbPassword="$NEXTCLOUD_PASSWORD"
```
