## traefik for HA

### install consul

```shell
helm install --name consul --namespace kube-system stable/consul
```

### installing traefik chart

```shell
envsubst < values.yaml >! tmp_values.yaml && helm install --name traefik --namespace kube-system --values tmp_values.yaml stable/traefik && rm tmp_values.yaml
```

### upgrading the traefik chart

```shell
envsubst < values.yaml >! tmp_values.yaml && helm upgrade traefik --values tmp_values.yaml stable/traefik && rm tmp_values.yaml
```

Regarding [values.yaml](values.yaml): Hard-coded the nodePorts so I don't need to keep changing haproxy's config.
