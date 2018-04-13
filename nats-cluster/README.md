# nats-cluster
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for creating
nats-cluster by using [nats-operator](https://github.com/nats-io/nats-operator/) 

# Managing the chart
The [nats-operator]() helm chart has to be installed first. 

## Install
```
helm install --name dev-release nats-cluster --namespace dictybase
```

For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).
__Make sure__ both operator and cluster gets installed in the same `namespace`

## Uninstall
```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **nats-cluster** chart and their default values.

| Parameter             | Description                | Default          |
| ----------------------|----------------------------|------------------|
| `image.nats.version`  | nats server image version  | `1.1.0`          |
| `cluster.size`        | no of nats server          | `0.2.0-v1alpha2` |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. 

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml nats-cluster --namespace dictybase
```
