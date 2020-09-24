# dictybase-configuration

This [Helm](https://github.com/kubernetes/helm) chart provides
[Kubernetes](http://kubernetes.io) manifests for setting up
dictybase-configuration.

## Credentials

A Kubernetes [secret](http://kubernetes.io/docs/user-guide/secrets/) is used for
storing the database credentials and any secret tokens.

## Auth secrets

When installing this chart, it is necessary to pass the required auth files through the command line like so:

```shell
helm install dictybase-configuration -n dictybase-configuration --set auth.privatekey=$(base64 -w0 app.rsa) \
--set auth.publickey=$(base64 -w0 app.rsa.pub) --set auth.config=$(base64 -w0 app.json)
```

# Managing the chart

## Install

```
helm install dictybase-configuration -n dictybase-configuration
```

For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall

```
helm uninstall dictybase-configuration
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **dictybase-configuration** chart and their default values.

| Parameter               | Description                                               | Default         |
| ----------------------- | --------------------------------------------------------- | --------------- |
| `arangodb.user`         | ArangoDB Admin User                                       | ``              |
| `arangodb.password`     | ArangoDB User Password                                    | ``              |
| `arangodb.databases`    | List of ArangoDB databases                                | See values.yaml |
| `endpoints.organism`    | JSON location for organism data (used for downloads page) | ``              |
| `endpoints.publication` | Publication API endpoint                                  | ``              |
| `minio.accesskey`       | Minio Access Key                                          | ``              |
| `minio.secretkey`       | Minio Secret Key                                          | ``              |
| `slack.token`           | Slack API token                                           | ``              |

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install dictybase-configuration -n dictybase-configuration -f values.yaml
```
