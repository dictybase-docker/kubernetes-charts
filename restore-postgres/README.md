# authserver
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for restoring a postgresql
database from archive.

## Credentials
A kubernetes [secret](http://kubernetes.io/docs/user-guide/secrets/)
`postgres-credentials` have to present or created in the cluster. It is the
same credentials that has to be created for the
[chado-postgresql](https://github.com/dictybase-docker/kubernetes-charts/tree/master/chado-postgres)
chart. Follow the documentation over
[there](https://github.com/dictybase-docker/kubernetes-charts/tree/master/chado-postgres).
