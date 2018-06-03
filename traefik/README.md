## traefik 

### using helm & custom fork
* Want to use traefik as a [HA cluster](https://docs.traefik.io/user-guide/cluster/)
* There is an [open PR](https://github.com/kubernetes/charts/pull/5563) to support consul in traefik for the official helm chart.
* Cloned this repo https://github.com/medialaan/k8s-charts-kubernetes.git and ran the following commands inside `stable/traefik`:

```
helm repo index .
helm serve . &
helm install --name traefik --namespace kube-system --values ~/traefik_values.yaml local/traefik
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

**Any external services that rely on websocket communication need to have their ingress annotation set to `traefik.frontend.passHostHeader: "true"`**  It appears that when traefik attempts to proxy websockets with this set to false, it causes all of the traefik pods to crash.

