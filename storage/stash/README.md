# stash for backing-up persistent storage volumes and cluster data

https://appscode.com/products/stash/

## Install Stash

### Install the 'onessl' CLI tool

```shell
# Mac OSX amd64:
curl -fsSL -o onessl https://github.com/kubepack/onessl/releases/download/0.3.0/onessl-darwin-amd64 \
  && chmod +x onessl \
  && sudo mv onessl /usr/local/bin/

# Linux amd64:
curl -fsSL -o onessl https://github.com/kubepack/onessl/releases/download/0.3.0/onessl-linux-amd64 \
  && chmod +x onessl \
  && sudo mv onessl /usr/local/bin/
```

### Install the stash helm chart

```shell
helm install appscode/stash --name stash-operator --version 0.7.0 \
  --set apiserver.ca="$(onessl get kube-ca)" \
  --set apiserver.enableValidatingWebhook=true \
  --set apiserver.enableMutatingWebhook=true
```

### Create the stash restic secret for later use

```shell
kubectl create secret generic restic-secret --from-literal=RESTIC_PASSWORD=${RESTIC_PASSWORD}
```

## Example usage

For a given deployment (named `wordpress`), the following example will backup the `/var/www/html` directory inside the `wordpress` pod matching the `app: wordpress` and `tier: frontend` **POD LABELS**.

The backup will land in the [`nfs-backup-restic-pv` PersistentVolume](../nfs-pv/backup-restic-pv.yaml) which lives on the NAS inside `/tank/backups/restic`.  The actual backup for this example will be in `/tank/backups/restic/deployment/wordpress/` and will backup every 5 minnutes and keep the last 5 backups.

```yaml
apiVersion: stash.appscode.com/v1alpha1
kind: Restic
metadata:
  name: stash-wordpress
  namespace: default
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: frontend
  fileGroups:
  - path: /var/www/html
    retentionPolicyName: 'keep-last-5'
  backend:
    local:
      mountPath: /mnt/backup/
      persistentVolumeClaim:
          claimName: nfs-backup-restic-pv
    storageSecretName: restic-secret
  schedule: '@every 5m'
  volumeMounts:
  - mountPath: /var/www/html
    name: wordpress-persistent-storage
  retentionPolicies:
  - name: 'keep-last-5'
    keepLast: 5
    prune: true
```
