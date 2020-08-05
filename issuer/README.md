# issuer

This [Helm](https://github.com/kubernetes/helm) chart provides
[Kubernetes](http://kubernetes.io) manifests for creating issuers and certificates.

# Managing the chart

## Prequisites

Deployments:

- [Cert Manager](https://github.com/jetstack/cert-manager)

## Install

```
helm install --name dev-release issuer
```

For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall

```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **issuer** chart and their default values.

| Parameter             | Description                         | Default                                                  |
| --------------------- | ----------------------------------- | -------------------------------------------------------- |
| `namespace`           | Namespace for all deployments       | ``                                                       |
| `issuer.name`         | Name of issuer                      | ``                                                       |
| `issuer.server`       | Letsencrypt server URL              | `https://acme-staging-v02.api.letsencrypt.org/directory` |
| `issuer.email`        | Personal email address              | ``                                                       |

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml issuer
```
