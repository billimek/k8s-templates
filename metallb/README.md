# MetalLB

https://metallb.universe.tf/installation/

## installation

This installs MetaLB using the layer2 mode with reserved service IPs being 10.0.6.10-10.0.6.250.

```shell
helm upgrade --install metallb stable/metallb --reset-values -f values.yaml
```

The router & haproxy LB needs associated changes to leverage the services at the new IP addresses.  For example:

* Traefik: The router is still sending all ingressing traffic for port 80 and port 443 to the load-balanced haproxy cluster.  The haproxy cluster, in turn, handles the traffic and for all things deemed necessary for traefik, forwards to 10.0.7.80 (the traefik service IP)
* Unifi: The router forwards the controller, stun, and discovery ingressed traffic directly to the Unifi LoadBalancer service IPs (10.0.7.82, 10.0.7.83, and 10.0.7.84 respectivley)
* InfluxDB: The load-balanced haproxy cluster is still handling all of the 8086 and 4242 traffic and forwarding to the LoadBalancer service IP (10.0.7.82). At some point, may route all clients to 10.0.7.82 directly.
