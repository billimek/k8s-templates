## Documentation for a personal kubernetes cluster

![](https://i.imgur.com/GcpsXlH.png)

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

1. [kubernetes-dashboard](kubernetes-dashboard/) - creating the kubernetes-dashboard
1. [helm](helm/) - set-up helm
1. [heapster](heapster/) - standing-up a heapster deployment for the dashboard to use for deeper metrics
1. [secrets](secrets/) - for creating secrets used in the cluster
1. [metallb](metallb/) - bare-metal LoadBalancer solution
1. [external-ceph](storage/external-ceph/) - external ceph replicated storage for HA
1. [nfs-client](storage/nfs-client/) - nfs-based dyanmic storage class for deployments to use
1. [nfs-pv](storage/nfs-pv/) - nfs-based persistent volumes for media nd data mounts from NAS
1. [stash](storage/stash/) - using stash to backup volumes
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
* [digitalocean-dyndns](/deployments/digitalocean-dyndns)
* [unifi](/deployments/unifi)
* [home-assistant](/deployments/home-assistant)
* [node-red](/deployments/node-red)
* [minio](/deployments/minio)
* [logging](/deployments/logging)
* [nextcloud](/deployments/nextcloud)

## Miscellaneous

* [arm](arm/) - **NOT CURRENTLY USING** experiment to run a k8s node on a raspberry pi
* [longhorn](storage/longhorn/) - **NOT CURRENTLY USING** experimental longhorn replicated storage solution with rancher
* [rook](storage/rook/) - **NOT CURRENTLY USING** rook ceph replicated storage for HA
