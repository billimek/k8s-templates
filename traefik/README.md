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
envsubst < traefik_values.yaml >! out.yaml && helm install --name traefik --namespace kube-system --values out.yaml local/traefik
```

Regarding [traefik_values.yaml](traefik_values.yaml): Hard-coded the nodePorts so I don't need to keep changing haproxy's config.


### properly referencing external services

The latest release of traefik has a [bug](https://github.com/containous/traefik/issues/1816) that doesn't allow proper references to externalName resources listening on custom ports. There is a [merged PR](https://github.com/containous/traefik/pull/3231) that fixes this issue but it is not yet built into an official release of traefik. For now, this requires adding the following to the `traefik_values.yaml` file for the custom traefik helm chart:

```
image: containous/traefik
imageTag: c37b040217435c1f1683fa7466b6d4ac3002d878
```

the `imageTag: c37b040217435c1f1683fa7466b6d4ac3002d878` represents the custom docker build of the commit sha with the bugfix for PR https://github.com/containous/traefik/pull/3231.

Once the next official release of traefik is shipped (with this fixed code) we can revert to the traefik:latest image or some variant.
