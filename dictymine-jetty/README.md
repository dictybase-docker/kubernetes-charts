# dictymine-jetty
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[jetty](https://hub.docker.com/_/jetty/)


# Managing the chart
## Install
```
helm install --name dev-release dictymine-postgres
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
| `image.repository`         | jetty image                                | `jetty`                                                    |
| `image.tag`                | `jetty` image tag                          | `9.4.4-jre8-alpine`                                        |
| `image.pullPolicy`         | Image pull policy                          | `IfNotPresent`                                             |
| `service.name`             | Name of the service.                       | `dictymine-jetty`                                          |
| `service.type`             | Type of service.                           | `ClusterIP`                                                |
| `service.externalPort`     | Accessible port of service.                | `8080`                                                     |
| `service.internalPort`     | Internal port of pod                       | `8080`                                                     |
| `resources.enabled`        | Activate resource configuration            | `false`                                                    |
| `resources.limits`         | Resource limits(maximum)                   |  cpu:`100m`, memory: `128mi`                               |
| `resources.requests`       | Resource requests(minimum)                 |  cpu:`100m`, memory: `128mi`                               |

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
