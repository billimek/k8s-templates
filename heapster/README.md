## heapster for metrics on the dashboard 

```
helm install --name heapster --namespace kube-system stable/heapster --values values.yaml
```

### kubernetes 1.11+ issue

Starting in kubernetes 1.11, the 'read only port' (10255) is disabled byb default.  This [breaks heapster](https://github.com/kubernetes/heapster/issues/2072) (and probably other things too).  I could never find a good solution to this, except to re-enable the port on the kubelet on each of the hosts.

On each k8s host, edit `/etc/default/kubelet` and add `--read-only-port 10255` to `KUBELET_EXTRA_ARGS`.  Then `service kubelet restart`
