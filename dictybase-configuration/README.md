# dictybase-configuration

This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for setting up
dictybase-configuration

## Credentials

Kubernetes [secret](http://kubernetes.io/docs/user-guide/secrets/) is used for
storing the database credentials.

## Auth secrets

When installing this chart, it is necessary to pass the required auth files through the command line like so:

```
helm install --name dev-release dictybase-configuration --set auth.privatekey=$(base64 -w0 app.rsa) --set auth.publickey=$(base64 -w0 app.rsa.pub) --set auth.config=$(base64 -w0 app.json)
```

# Managing the chart

## Install

```
helm install --name dev-release dictybase-configuration
```

For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall

```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration
