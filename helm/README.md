## installing helm

From [this guide](https://joshrendek.com/2018/04/kubernetes-on-bare-metal/):

```shell
kubectl create -f helm-rbac.yaml
kubectl create serviceaccount --namespace kube-system tiller
helm init --upgrade
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
```
