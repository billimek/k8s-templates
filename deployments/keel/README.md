## keel

```bash
helm install --name keel stable/keel --namespace kube-system --values values.yaml --set slack.token="$KEEL_SLACK_TOKEN"
```

### May be needed to make keel work properly

```shell
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default
```