## keel

```bash
helm install --name keel stable/keel --namespace kube-system --values values.yaml --set slack.token="$KEEL_SLACK_TOKEN"
```
