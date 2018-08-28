## nfs-based persistent mouts for various pod access (media mount & data mount)

```shell
kubectl apply -f media-pv.yaml
kubectl apply -f data-pv.yaml
kubectl apply -f data-nextcloud-pv.yaml
kubectl apply -f media-audiobooks-pv.yaml
```