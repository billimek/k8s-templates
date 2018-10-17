# traefik for HA

## consul for k/v store for multi-node traefik support

### install the consul chart

```shell
helm install --name consul --namespace kube-system stable/consul --values consul_values.yaml --set uiIngress.hosts="{consul.k.$DOMAIN}"
```

### upgrade the consul chart

```shell
helm upgrade consul --namespace kube-system stable/consul --reset-values --values consul_values.yaml --set uiIngress.hosts="{consul.k.$DOMAIN}"
```

## traefik

### installing traefik chart

```shell
envsubst < values.yaml >! tmp_values.yaml && helm install --name traefik --namespace kube-system --values tmp_values.yaml stable/traefik && rm tmp_values.yaml
```

### upgrading the traefik chart

```shell
envsubst < values.yaml >! tmp_values.yaml && helm upgrade traefik --reset-values --values tmp_values.yaml stable/traefik && rm tmp_values.yaml
```

Regarding [values.yaml](values.yaml): Hard-coded the nodePorts so I don't need to keep changing haproxy's config.
