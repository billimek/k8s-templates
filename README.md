## Documentation for a personal kubernetes cluster

## Building the cluster
Refer to the [cluster](cluster/) - cluster build-out information

## kubectl and variable subsitution
A local .gitignoreed `.env` file contains things like:

```
export EMAIL="someone@somedomain.com"
export DOMAIN="somedomain.com"
export TRAEFIK_AUTH="username: somesecretmd5"
```

Use `envsubst` at `kubectl` runtime to subsitute these with the proper values.  For example,

```
source .env
envsubst < traefik/external/sonarr/external_sonarr.yaml | kubectl apply -f -
```

Otherwise, leverage helm charts and the built-in helm value-substitution mechanism.

## Installing the core system components
Refer to and follow the following:

1. [kubernetes-dashboard](kubernetes-dashboard/) - creating the kubernetes-dashboard
1. [helm](helm/) - set-up helm
1. [heapster](heapster/) - standing-up a heapster deployment for the dashboard to use for deeper metrics
1. [secrets](secrets/) - for creating secrets used in the cluster
1. [rook](rook/) - rook-ceph storage cluster for all the things to use for storage
1. [consul](consul/) - consul KV store (using rook) for traefik to persist cert data in a HA deployment
1. [traefik](traefik/) - traefik ingress & reverse proxy


## Installing the default runtime components

1. TBD

## Miscellaneous

* [arm](arm/) - experiment to run a k8s node on a raspberry pi