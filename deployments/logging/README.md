# EFK Stack (elasticsearch, fluent-bit, kibana)

## install

```shell
helm install --name elasticsearch stable/elasticsearch --values elasticsearch-values.yaml
helm install --name fluent-bit stable/fluent-bit --values fluent-bit-values.yaml
helm install --name kibana stable/kibana --values kibana-values.yaml --set ingress.hosts="{kibana.$DOMAIN}"
```

## upgrade

```shell
helm upgrade elasticsearch stable/elasticsearch --reset-values --values elasticsearch-values.yaml
helm upgrade fluent-bit stable/fluent-bit --reset-values --values fluent-bit-values.yaml
helm upgrade kibana stable/kibana --reset-values --values kibana-values.yaml --set ingress.hosts="{kibana.$DOMAIN}"
```

## backup (stash)

```shell
kubectl create -f elasticsearch-stash.yaml
```
