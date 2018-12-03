# EFK Stack (elasticsearch, fluent-bit, kibana)

![](https://i.imgur.com/HiHZpMa.png)

## install

```shell
helm install --name elasticsearch billimek/elasticsearch --values elasticsearch-values.yaml
helm install --name fluent-bit stable/fluent-bit --values fluent-bit-values.yaml
helm install --name kibana stable/kibana --values kibana-values.yaml --set ingress.hosts="{kibana.$DOMAIN}"
helm install --name elasticsearch-curator stable/elasticsearch-curator --set config.elasticsearch.hosts="{elasticsearch}"
```

### logtrail

Install logtrail 'settings' by uploading them to elasticsearch directly:

```shell
kubectl port-forward service/elasticsearch 9200:9200 &
curl -XPUT 'localhost:9200/.logtrail/config/1?pretty' -H 'Content-Type: application/json' -d@logtrail.json
```

(requires a restart of kibana to pick-up changes)

## upgrade

```shell
helm upgrade elasticsearch billimek/elasticsearch --reset-values --values elasticsearch-values.yaml
helm upgrade fluent-bit stable/fluent-bit --reset-values --values fluent-bit-values.yaml
helm upgrade kibana stable/kibana --reset-values --values kibana-values.yaml --set ingress.hosts="{kibana.$DOMAIN}"
helm install --upgrade elasticsearch-curator stable/elasticsearch-curator --set config.elasticsearch.hosts="{elasticsearch}"
```

## backup (stash)

```shell
kubectl create -f elasticsearch-stash.yaml
```

## Miscellaneous

If the elasticsearch cluster somehow becomes read-only (i.e. low disk space), it will not automatically switch-back when you address the issue.  Instead, 'flip' it back by:

```shell
kubectl port-forward service/elasticsearch 9200:9200 &
curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'
```
