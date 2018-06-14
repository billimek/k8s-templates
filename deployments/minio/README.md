## minio

```bash
helm install --name minio stable/minio --values values.yaml --set accessKey="$MINIO_ACCESS_KEY",secretKey="$MINIO_SECRET_KEY",ingress.hosts="{minio.$DOMAIN}"
```