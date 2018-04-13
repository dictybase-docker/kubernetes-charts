# arangodb
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running [arangodb](http://arangodb.com)
using [arango-operator](https://github.com/arangodb/kube-arangodb/blob/master/docs/Manual/Deployment/Kubernetes/Usage.md#installation).

# Managing the chart
__Make sure__ the `arango-operator` is installed first.

## Install
```
helm install --name dev-release arangodb 
```
For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall
```
helm uninstall dev-release   
```
For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **arangodb** chart and their default values.

| Parameter                         | Description                   | Default                    |
| ----------------------------------|-------------------------------|----------------------------|
| `image.repository`                | image repository              | `arangodb/arangodb`        |
| `image.tag`                       | image tag                     | `3.3.7`                    |
| `image.pullPolicy`                | Image pull policy             | `IfNotPresent`             |
| `arangodb.mode`                   | Type of deployment            | `ResilientSingle`          |
| `arangodb.environment`            | Environment for deploy        | `Development`              |
| `arangodb.engine`                 | Storage engine                | `RocksDB`                  |
| `arangodb.agents.count`           | No of agents                  | `3`                        |
| `arangodb.agents.storage`         | Storage for each agent        | `500Mi`                    |
| `arangodb.dbservers.storage`      | Storage for each dbservers    | `500Mi`                    |


Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml arangodb
```
