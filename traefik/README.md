# traefik for HA

![](https://i.imgur.com/gwienvX.png)

## consul for k/v store for multi-node traefik support

### install the consul chart

```shell
helm install --name consul --namespace kube-system stable/consul --values consul_values.yaml --set uiIngress.hosts="{consul.k.$DOMAIN}"
```

### upgrade the consul chart

```shell
helm upgrade consul --namespace kube-system stable/consul --reset-values --values consul_values.yaml --set uiIngress.hosts="{consul.k.$DOMAIN}"
```

### backup (stash)

```shell
kubectl create -f stash.yaml
```

## traefik

### installing traefik chart

```shell
envsubst < values.yaml >! tmp_values.yaml && helm install --name traefik --namespace kube-system --values tmp_values.yaml stable/traefik && rm tmp_values.yaml
```

### upgrading the traefik chart

```shell
envsubst < values.yaml >! tmp_values.yaml && helm upgrade traefik --reset-values --values tmp_values.yaml stable/traefik && rm tmp_values.yaml
```

Regarding [values.yaml](values.yaml): Hard-coded the nodePorts so I don't need to keep changing haproxy's config.

### set-up ingresses for external services

```shell
for i in external/*/*.yaml
do
kapply $i
done
```

## auth0 oauth forwarder

### configure auth0 site

#### generic application setup

Create a generic 'application' with the following set as _Allowed Callback URLs_:

* https://auth.mydomain.com
* https://auth.mydomain.com/signin
* https://auth.mydomain.com/login/callback

Use the generated Client ID & Client Secret in the `auth0-forwardauth-values.yaml` configuration below

#### email domain whitelist rule

Create a new 'rule' for _Email domain whitelist_ with the following modifications to redirect authorization failures to a static site:

```js
function (user, context, callback) {

  // Access should only be granted to verified users.
  if (!user.email || !user.email_verified) {
    return callback(null, user, context);
  }

  const whitelist = ['somedomain.com', 'someotherdomain.com']; //authorized domains
  const userHasAccess = whitelist.some(
      function (domain) {
        const emailSplit = user.email.split('@');
        return emailSplit[emailSplit.length - 1].toLowerCase() === domain;
      });

  if (!userHasAccess) {
    context.redirect = {
        url: "<some static page>"
    };
    return callback(null, user, context);
    //return callback(new UnauthorizedError('Access denied.'));
  }

  return callback(null, user, context);
}
```

### installing traefik-forward-auth0 chart

Until [PRs](https://github.com/dniel/traefik-forward-auth0/pulls) are merged, directly referencing the `integration` branch of my [fork of this](https://github.com/billimek/traefik-forward-auth0)

```shell
helm upgrade --install auth0 --values auth0-forwardauth-values.yaml ../../traefik-forward-auth0/helm/ --set ingress.hosts="{auth.$DOMAIN}"
```
