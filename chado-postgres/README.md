# chado-postgres
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[chado-postgresql](https://hub.docker.com/r/dictybase/chado-postgres/).

## Credentials
Kubernetes [secret](http://kubernetes.io/docs/user-guide/secrets/) is used for
storing the database credentials. The secret manifest is deployed as
[pre-install
hook](https://github.com/kubernetes/helm/blob/master/docs/charts_hooks.md).

# Managing the chart
## Install
```
helm install --name dev-release chado-postgres
```

For details, look [here](https://github.com/kubernetes/helm/blob/master/docs/using_helm.md#helm-install-installing-a-package).

## Uninstall
```
helm uninstall dev-release
```

For details, look [here](https://github.com/kubernetes/helm/blob/master/docs/using_helm.md#helm-delete-deleting-a-release).

For upgrades and rollback, look [here](https://github.com/kubernetes/helm/blob/master/docs/using_helm.md#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).


## Configuration

The following tables lists the configurable parameters of the chado-postgres chart and their default values.

| Parameter                  | Description                                | Default                                                    |
| -----------------------    | ----------------------------------         | ---------------------------------------------------------- |
| `imageTag`                 | `postgres` image tag                       | `1.0.0`                                                    |
| `imagePullPolicy`          | Image pull policy                          | `Always` if `imageTag` is `latest`, else `IfNotPresent`    |
| `postgresUser`             | Username of new user to create.            | `postgres`                                                 |
| `postgresPassword`         | Password for the new user.                 | random 10 characters                                       |
| `postgresDatabase`         | Name for new database to create.           | `postgres`                                                 |
| `chadoUser`                | Username of a regular user to create.      | `chadomaster`                                              |
| `chadoPassword`            | Password for the regulsr user.             | random 12 characters                                       |
| `chadoDatabase`            | Name for new user database to create.      | `dictychado`                                               |
| `serviceName`              | Name of the service.                       | `postgresql`                                               |
| `serviceType.enabled`      | Explicitly specify the service type.       | `false`                                                    |
| `serviceType.name`         | Type of service.                           | `NodePort`                                                 |
| `persistence.enabled`      | Use a PVC to persist data                  | `true`                                                     |
| `persistence.storageClass` | Storage class of backing PVC               | `nil` (uses alpha storage class annotation)                |
| `persistence.accessMode`   | Use volume as ReadOnly or ReadWrite        | `ReadWriteOnce`                                            |
| `persistence.size`         | Size of data volume                        | `8Gi`                                                      |
| `persistence.subPath`      | Subdirectory of the volume to mount at     | `postgresql-db`                                            |
| `metrics.enabled`          | Start a side-car prometheus exporter       | `false`                                                    |
| `metrics.image`            | Exporter image                             | `wrouesnel/postgres_exporter`                              |
| `metrics.imageTag`         | Exporter image                             | `v0.1.1`                                                   |
| `metrics.imagePullPolicy`  | Exporter image pull policy                 | `IfNotPresent`                                             |
| `metrics.resources`        | Exporter resource requests/limit           | Memory: `256Mi`, CPU: `100m`                               |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set postgresUser=my-user,postgresPassword=secretpassword,postgresDatabase=my-database \
    stable/postgresql
```
The above command creates a PostgresSQL user named `root` with password `secretpassword`. Additionally it creates a database named `my-database`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml stable/postgresql
```
