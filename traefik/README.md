## traefik 

### installing local fork of traefik
(inside the [fork of the helm chafrts repo](https://github.com/billimek/charts)):

```
cd charts/stable
helm package traefik
helm serve . &
```

### installing traefik chart

```
envsubst < values.yaml >! tmp_values.yaml && helm install --name traefik --namespace kube-system --values tmp_values.yaml billimek/traefik && rm tmp_values.yaml
```

### upgrading the traefik chart

```
envsubst < values.yaml >! tmp_values.yaml && helm upgrade traefik --values tmp_values.yaml billimek/traefik && rm tmp_values.yaml
```

Regarding [values.yaml](values.yaml): Hard-coded the nodePorts so I don't need to keep changing haproxy's config.
