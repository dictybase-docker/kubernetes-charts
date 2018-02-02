# chado-sqitch
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[chado-sqitch](https://hub.docker.com/r/dictybase/chado-sqitch/).

# Managing the chart
## Install
```
helm install --name dev-release chado-sqitch
```

For details, look
[here](https://github.com/kubernetes/helm/blob/master/docs/using_helm.md#helm-install-installing-a-package).

## Uninstall
```
helm uninstall dev-release
```

For details, look
[here](https://github.com/kubernetes/helm/blob/master/docs/using_helm.md#helm-delete-deleting-a-release).

For upgrades and rollback, look
[here](https://github.com/kubernetes/helm/blob/master/docs/using_helm.md#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).


## Configuration

The following tables lists the configurable parameters of the **chado-sqitch** chart and their default values.

| Parameter                        | Description                                                | Default                                                   |
| ---------------------------------|------------------------------------------------------------| ----------------------------------------------------------|
| `image.repository`               | chado-sqitch image                                         | `dictybase/chado-sqitch`                                  |
| `image.tag`                      | image tag                                                  | `v1.23.5`                                                 |
| `image.pullPolicy`               | Image pull policy                                          | `Always` if `imageTag` is `latest`, else `IfNotPresent`   |
| `chadoPostgres.config.name`      | Name of the `ConfigMap` that has database config values    | `chado-postgres`                                          |
| `chadoPostgres.config.database`  | Name of the `ConfigMap` key with database name             | `chado.database`                                          |
| `chadoPostgres.config.user`      | Name of the `ConfigMap` key with user name                 | `chado.user`                                              |
| `chadoPostgres.secrets.name`     | Name of the `Secrets` that has database credentials        | `chado-postgres`                                          |
| `chadoPostgres.secrets.password` | Name of the `Secrets` key with database password           | `chado-password`                                          |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. 

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml stable/postgresql
```
