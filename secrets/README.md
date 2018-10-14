## secrets

Followed [this guide](https://docs.traefik.io/user-guide/kubernetes/#creating-the-secret) to create the secret for traefik to reference:

```shell
kubectl create secret generic traefik-basic-auth-jeff --from-file auth --namespace kube-system
kubectl create secret generic traefik-basic-auth-jeff --from-file auth
```