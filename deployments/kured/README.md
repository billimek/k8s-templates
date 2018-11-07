# kured

## install/upgrade

```shell
helm upgrade --install kured --namespace kube-system stable/kured --reset-values --values values.yaml --set extraArgs.slack-hook-url="$SLACK_WEBHOOK_URL"
```