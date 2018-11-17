# ark

## installation

Must have previously installed [minio](../../deployments/minio/)

```shell
k create -f 00-prereqs.yaml
kapply 00-secrets.yaml
kapply 05-ark-backupstoragelocation.yaml
k create -f 20-ark-deployment.yaml
k create -f 30-restic-daemonset.yaml
```

Install the 'ark' CLI from https://github.com/heptio/ark/releases


## backing-up

### creating one-off backup

`ark backup create k8s`

### creating a scheduled backup

`ark schedule create k8s --schedule="@daily"`

### viewing backups

```shell
❯ ark backup get
NAME                 STATUS      CREATED                         EXPIRES   SELECTOR
k8s                  Completed   2018-11-02 02:52:01 +0000 UTC   29d       <none>
k8s-20181102031955   Completed   2018-11-02 03:19:55 +0000 UTC   29d       <none>
```