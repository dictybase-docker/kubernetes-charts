# nats-operator
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for creating
[nats-operator](https://github.com/nats-io/nats-operator/) using [Custom
Resource
Definiton](https://kubernetes.io/docs/concepts/api-extension/custom-resources/#customresourcedefinitions)
(CRD)

# Managing the chart
## Install
```
helm install --name dev-release nats-operator --namespace dictybase
```
For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall
```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **nats-operator** chart and their default values.

| Parameter           | Description           | Default                            |
| --------------------|-----------------------|------------------------------------|
| `image.repository`  | operator image        | `connect-everything/nats-operator` |
| `image.tag`         | image tag             | `0.2.0-v1alpha2`                   |
| `image.pullPolicy`  | Image pull policy     | `Always`                           |
| `operator.name`     | Name of the operator  | `nats-operator`                    |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. 

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml nats-operator --namespace dictybase
```
