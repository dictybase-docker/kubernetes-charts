# argo-pipeline

This [Helm](https://github.com/kubernetes/helm) chart provides
[Kubernetes](http://kubernetes.io) manifests for running [Argo](https://argoproj.github.io/docs/argo/readme.html)
and [Argo Events](https://argoproj.github.io/argo-events/) with our development
pipelines.

# Managing the chart

## Prequisites

Deployments:

- [Argo](https://github.com/argoproj/argo-helm/tree/master/charts/argo)
- [Argo Events](https://github.com/argoproj/argo-helm/tree/master/charts/argo-events)

Make sure that both are installed in the same namespace (`argo`). Argo also needs
to be configured to use Minio as an artifact repository, and it should use the `argo-workflow`
rbac.

You need to create three [Kubernetes secrets](https://kubernetes.io/docs/concepts/configuration/secret/):

- Slack

> `$_> kubectl create secret generic slack-secret -n argo \`  
>  `--from-literal=oauth-token=YOUR_TOKEN_HERE...`

- GitHub

> `$_> kubectl create secret generic github-access -n argo \`  
>  `--from-literal=apiToken=YOUR_TOKEN_HERE... \`  
>  `--from-literal=webHookSecret=YOUR_SECRET_HERE...`

- Docker

> `$_> kubectl create secret generic docker-secret -n argo \`  
>  `--from-file=${HOME}/.docker/config.json`

You also need to set up Ingress for your `github-gateway`. See [here](https://github.com/dictyBase/Migration/blob/master/deployment/argoevents.md#ingress).

## Install

```
helm install --name dev-release argo-pipeline
```

For details, look [here](https://docs.helm.sh/using_helm/#helm-install-installing-a-package).

## Uninstall

```
helm uninstall dev-release
```

For details, look [here](https://docs.helm.sh/using_helm/#uninstall-a-release).

For upgrades and rollback, look [here](https://docs.helm.sh/using_helm/#helm-upgrade-and-helm-rollback-upgrading-a-release-and-recovering-on-failure).

## Configuration

The following tables lists the configurable parameters of the **argo-pipeline** chart and their default values.

| Parameter                         | Description                                | Default                          |
| --------------------------------- | ------------------------------------------ | -------------------------------- |
| `namespace`                       | Namespace for all deployments              | `argo`                           |
| `serviceAccount`                  | ServiceAccount for Argo Events             | `argo-events-sa`                 |
| `gateway.name`                    | Name of gateway                            | `github-gateway`                 |
| `gateway.ports.servicePort`       | Service port for gateway                   | `12000`                          |
| `gateway.ports.targetPort`        | Target port for gateway                    | `12000`                          |
| `gateway.ports.type`              | Type of port for gateway                   | `NodePort`                       |
| `gateway.processorPort`           | Processor port for gateway                 | `9330`                           |
| `gateway.eventProtocol.type`      | Type of gateway event protocol             | `HTTP`                           |
| `gateway.eventProtocol.port`      | Port for gateway event protocol            | `9300`                           |
| `eventSource.name`                | Name of event source                       | `github-event-source`            |
| `eventSource.owner`               | Repository owner                           | `dictyBase`                      |
| `eventSource.hookURL`             | URL base for webhooks                      | `https://ericargo.dictybase.dev` |
| `eventSource.apiToken.name`       | Name of K8s secret with token              | `github-access`                  |
| `eventSource.apiToken.key`        | Key containing GitHub access token         | `apiToken`                       |
| `eventSource.webHookSecret.name`  | Name of K8s secret with webhook secret     | `github-access`                  |
| `eventSource.webHookSecret.key`   | Key containing GitHub webhook secret       | `webHookSecret`                  |
| `eventSource.events`              | Array of GitHub events to trigger webhooks | `[push]`                         |
| `sensor.backendName`              | Name of backend sensor                     | `github-sensor`                  |
| `sensor.backendNoTestName`        | Name of sensor for backend without tests   | `github-sensor`                  |
| `sensor.frontendName`             | Name of frontend sensor                    | `github-sensor`                  |
| `sensor.frontendWorkflow`         | URL location of frontend workflow yaml     | `url`                            |
| `sensor.backendWorkflow`          | URL location of backend workflow yaml      | `url`                            |
| `sensor.backendNoTestWorkflow`    | URL of testless backend workflow yaml      | `url`                            |
| `sensor.verifyCert`               | Boolean for secure connection              | `false`                          |
| `hooks`                           | Array of webhooks (with repo and ID)       | `[]`                             |
| `frontend`                        | Array of all frontend repos with webhooks  | `[]`                             |
| `backend`                         | Array of all backend repos with webhooks   | `[]`                             |
| `backendNoTests`                  | Array of all backend repos without tests   | `[]`                             |
| `workflow.slackChannel`           | Slack channel to send notification         | `ericdev-ci`                     |
| `workflow.endpoint`               | Endpoint for Argo workflow                 | `url`                            |
| `workflow.srcPath`                | Src path for containers                    | `/src`                           |
| `workflow.arangoPass`             | ArangoDB password                          | `vandelay`                       |
| `workflow.dbVersion`              | ArangoDB version                           | `3.3.19`                         |
| `workflow.unitTestContainerImage` | Docker image for backend unit tests        | `dictybase/backend-tester`       |
| `workflow.frontendSrc`            | Src folder to use for frontend workflow    | `/code`                          |
| `workflow.frontendTag`            | Tag for frontend-builder Docker image      | `ericdev`                        |

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml argo-pipeline
```
