## heapster for metrics on the dashboard 

From [this guide](https://joshrendek.com/2018/04/kubernetes-on-bare-metal/):

```
helm install stable/heapster --name heapster --set rbac.create=true
```