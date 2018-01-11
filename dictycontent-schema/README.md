# chado-sqitch
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[dictycontent-schema](https://hub.docker.com/r/dictybase/dictycontent-schema/).

# Managing the chart
## Install
```
helm install --name dev-release dictycontent-schema
```

For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall
```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **chado-sqitch** chart and their default values.

| Parameter                               | Description                                                | Default                                                          |
| ---------------------------------       |------------------------------------------------------------| ----------------------------------------------------------       |
| `image.repository`                      | dictycontent-schema image                                  | `dictybase/dictycontent-schema`                                  |
| `image.tag`                             | image tag                                                  | `v1.0.0`                                                         |
| `image.pullPolicy`                      | Image pull policy                                          | `IfNotPresent`                                                   |
| `dictyContentPostgres.config.name`      | Name of the `ConfigMap` that has database config values    | `dictycontent-postgres`                                          |
| `dictyContentPostgres.config.database`  | Name of the `ConfigMap` key with database name             | `dictycontent.database`                                          |
| `dictyContentPostgres.config.user`      | Name of the `ConfigMap` key with user name                 | `dictycontent.user`                                              |
| `dictyContentPostgres.secrets.name`     | Name of the `Secrets` that has database credentials        | `dictycontent-postgres`                                          |
| `dictyContentPostgres.secrets.password` | Name of the `Secrets` that has database password           | `dictycontent.password`                                          |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. 

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml dictycontent-schema
```
