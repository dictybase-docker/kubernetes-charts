# dictyuser-postgres
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[dictyuser-postgresql](https://hub.docker.com/r/dictybase/dictyuser-postgres/).

## Credentials
Kubernetes [secret](http://kubernetes.io/docs/user-guide/secrets/) is used for
storing the database credentials. 

# Managing the chart
## Install
```
helm install --name dev-release dictyuser-postgres
```

For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall
```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).


## Configuration

The following tables lists the configurable parameters of the chado-postgres chart and their default values.

| Parameter                     | Description                                | Default                                         |
| -----------------------       | ----------------------------------         | ------------------------------------------------|
| `image.repository`            | postgresql image                           | `dictybase/dictyuser-postgres`               |
| `image.tag`                   | `dictyuser-postgres` image tag             | `v1.0.0`                                        |
| `image.pullPolicy`            | Image pull policy                          | `Always`                                        |
| `postgresUser`                | Username of new user to create.            | `postgres`                                      |
| `postgresPassword`            | Password for the new user.                 |  Required                                       |
| `postgresDatabase`            | Name for new database to create.           | `postgres`                                      |
| `postgresInitdbArgs`          | Initdb Arguments.                          | `--data-checksums`                              |
| `dictyuserUser`               | Username of a dictyuser user to create.    | `dictyusermaster`                               |
| `dictyuserPassword`           | Password for the dictyuser user.           |  Required                                       |
| `dictyuserDatabase`           | Name for dictyuser database to create.     | `dictyuser`                                     |
| `service.name`                | Name of the service.                       | `dictyuser-backend`                             |
| `service.type`                | Type of service.                           | `NodePort`                                      |
| `service.port`                | Port of service.                           | `5435`                                          |
| `persistence.enabled`         | Use a PVC to persist data                  | `true`                                          |
| `persistence.existingClaim`   | Use a PVC to persist data                  | `true`                                          |
| `persistence.storageClass`    | Storage class of backing PVC               | `nil` (uses alpha storage class annotation)     |
| `persistence.accessMode`      | Use volume as ReadOnly or ReadWrite        | `ReadWriteOnce`                                 |
| `persistence.annotations`     | Persistent Volume annotations              | `{}`                                            |
| `persistence.size`            | Size of data volume                        | `2Gi`                                           |
| `persistence.subPath`         | Subdirectory of the volume to mount at     | `dictyuser-db`                                  |
| `resources`                   | CPU/Memory resource requests/limits        |  `nil`                                          |
| `metrics.enabled`             | Start a side-car prometheus exporter       | `false`                                         |
| `metrics.image.repository`    | Exporter image                             | `wrouesnel/postgres_exporter`                   |
| `metrics.image.tag`           | Exporter image                             | `v0.4.1`                                        |
| `metrics.image.pullPolicy`    | Exporter image pull policy                 | `IfNotPresent`                                  |
| `metrics.resources`           | Exporter resource requests/limit           | Memory: `256Mi`, CPU: `100m`                    |
| `nodeSelector`                | Node labels for pod assignment             | {}                                              |
| `affinity`                    | Affinity settings for pod assignment       | {}                                              |
| `tolerations`                 | Toleration labels for pod assignment       | []                                              |

Specify each parameter using the `--set key=value[,key=value]` argument to
`helm install`. For example,

```bash
$ helm install --name my-release \
  --set postgresUser=my-user,postgresPassword=secretpassword,postgresDatabase=my-database \
  --set dictyuserPassword=django
   dictyuser-postgres
```
The above command creates a PostgresSQL user named `root` with password
`secretpassword` along a database named `my-database`. It also creates a
database `dictyuser` accessible by user `dictyusermaster` with password
`django`.

Alternatively, a YAML file that specifies the values for the parameters can be
provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml dictyuser-postgresql
```
