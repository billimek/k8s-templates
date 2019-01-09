## Documentation for a personal kubernetes cluster

![](https://i.imgur.com/FxTIC6p.png)

## Building the cluster
Refer to the [cluster](cluster/) - cluster build-out information

## kubectl and variable subsitution
A local .gitignoreed `.env` file contains things like:

```bash
export EMAIL="someone@somedomain.com"
export DOMAIN="somedomain.com"
export TRAEFIK_AUTH="username: somesecretmd5"
```

Use `envsubst` at `kubectl` runtime to subsitute these with the proper values.  For example,

Create `kapply` function to make this easier

```bash
kapply() {envsubst < "$@" | kubectl apply -f -}
```

```bash
source .env
kapply traefik/external/nvr/external_nvr.yaml
```

Otherwise, leverage helm charts and the built-in helm value-substitution mechanism.

## Installing the core system components
Refer to and follow the following:

1. [flux](flux/) - leverage flux-based GitOps to control cluster state.
1. [kubernetes-dashboard](kubernetes-dashboard/) - creating the kubernetes-dashboard
1. [heapster](heapster/) - standing-up a heapster deployment for the dashboard to use for deeper metrics
1. [metallb](metallb/) - bare-metal LoadBalancer solution
1. [storage](storage/) - storage solutions
1. [traefik](traefik/) - traefik ingress & reverse proxy

## Installing the default runtime components

* [keel](/deployments/keel)

* [influxdb](/deployments/influxdb)
* [chronograf](/deployments/chronograf)
* [grafana](/deployments/grafana)
* [prometheus](/deployments/prometheus)
* [hubot](/deployments/hubot)
* [comcast](/deployments/comcast)
* [speedtest](/deployments/speedtest)
* [modem-stats](/deployments/modem-stats)
* [uptimerobot](/deployments/uptimerobot)
* [unifi](/deployments/unifi)
* [home-assistant](/deployments/home-assistant)
* [node-red](/deployments/node-red)
* [minio](/deployments/minio)
* [logging](/deployments/logging)
* [nextcloud](/deployments/nextcloud)
* [deluge](/deployments/deluge)
* [rutorrent](/deployments/rutorrent)
* [nzbget](/deployments/nzbget)
* [radarr](/deployments/radarr)
* [sonarr](/deployments/sonarr)
* [plex](/deployments/plex)
* [minecraft](/deployments/minecraft)
* [kured](deployments/kured)
* [descheduler](deployments/descheduler)

## Miscellaneous

* [arm](arm/) - **NOT CURRENTLY USING** experiment to run a k8s node on a raspberry pi
