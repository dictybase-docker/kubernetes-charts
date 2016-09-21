# chado-postgres
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[chado-postgresql](https://hub.docker.com/r/dictybase/chado-postgres/).

## Credentials
A kubernetes [secret](http://kubernetes.io/docs/user-guide/secrets/) `postgres-credentials`
have to created. The default name`(postgres-credentials)` could be changed either
from the *values* file or setting it from helm command line. It is expected to have
the following keys.

* pgpass : password for **postgres** superuser, recommended. 
* adminuser: name of additional superuser, recommended. This account allows to do other administrative task using psql. 
* adminpass
* admindb
* chadouser: Additional user, primarily meant for using the chado schema.
* chadopass
* chadodb

### Example of creating secret
It is easier to create individual file for each secret key, put them in a directory and then create the secret off it.

```shell
kubectl create secret generic postgres-credentials --from-file=pg-credentials/
```

Or it could also be created from literal values

```shell
kubectl create secret generic postgres-credentials --from-literal=adminuser=admin \
    --from-literal=chadouser=chado ....
```


