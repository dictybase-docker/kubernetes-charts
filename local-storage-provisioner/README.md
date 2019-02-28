# local-storage-provisioner
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for creating
local hostpath based dynamic storage controller.

# Managing the chart
## Install
```
helm install --name dev-release local-storage-provisioner --set storage.path=/mnt/storage
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

| Parameter               | Description                       | Default                                   |
| ----------------------- | --------------------------------- | ------------------------------------------|
| `image.repository`      | storage provisioner image         | `gcr.io/k8s-minikube/storage-provisioner` |
| `image.tag`             | image tag                         | `v1.1.0`                                  |
| `image.pullPolicy`      | Image pull policy                 | `IfNotPresent`                            |
| `storage.path`          | Absolute host path                | __Required__                              |
| `className`             | Name of default storage class     |  `local-storage`                          |
