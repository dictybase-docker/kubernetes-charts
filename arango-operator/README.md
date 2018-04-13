# arango-operator
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for creating
[arango-operator](https://github.com/arangodb/kube-arangodb/blob/master/docs/Manual/Deployment/Kubernetes/Usage.md#installation)
using [Custom Resource
Definiton](https://kubernetes.io/docs/concepts/api-extension/custom-resources/#customresourcedefinitions)
(CRD). It manages deployment of ArangoDB database and provide
`PersistentVolumes` for local storage of your nodes. The second `CRD` is
optional.

# Managing the chart
## Install
```
helm install --name dev-release arango-operator --namespace dictybase
```
For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Status/Debug
To check if its running 

``` 
kubectl get crd -n dictybase
```

## Uninstall
```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **arango-operator** chart and their default values.

| Parameter              | Description           | Default                            |
| -----------------------|-----------------------|------------------------------------|
| `image.repository`     | operator image        | `arangodb/kube-arangodb`           |
| `image.tag`            | image tag             | `0.1.0`                            |
| `image.pullPolicy`     | Image pull policy     | `Always`                           |
| `operator.name`        | Name of the operator  | `arango-deployment-operator`       |
| `operator.allowChaos`  | Allow chaos           | `true`                             |


Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml arango-operator --namespace dictybase
```
