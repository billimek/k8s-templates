##Documentation for a personal kubernetes cluster

##Layout is as follows:

* [cluster](cluster/) - cluster build-out information
* [kubernetes-dashboard](kubernetes-dashboard/) - creating the kubernetes-dashboard
* [heapster](heapster/) - standing-up a heapster deployment for the dashboard to use for deeper metrics
* [helm](helm/) - leverage helm charts
* [rook](rook/) - rook-ceph storage cluster for all the things to use for storage
* [consul](consul/) - consul KV store (using rook) for traefik to persist cert data in a HA deployment
* [traefik](traefik/) - traefik ingress & reverse proxy
* [secrets](secrets/) - for creating secrets used in the cluster
* [arm](arm/) - experiment to run a k8s node on a raspberry pi
