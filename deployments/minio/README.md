## minio

![](https://i.imgur.com/RF0aYAg.png)

```bash
helm install --name minio stable/minio --values values.yaml --set accessKey="$MINIO_ACCESS_KEY",secretKey="$MINIO_SECRET_KEY",ingress.hosts="{minio.$DOMAIN}"
```
