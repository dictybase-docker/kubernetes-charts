# authserver
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[authserver](https://github.com/dictyBase/authserver).

## Credentials
A kubernetes [secret](http://kubernetes.io/docs/user-guide/secrets/) `auth-credentials`
have to created. It should have at least the following three keys.

* jwt-public-key
* jwt-private-key
* client-private-keys : This one should be a json encoded key pair
  values in the following format where each key represent a
  particular `oauth2` provider.

```json
{
  “google”: “secret-xxxxxxx”,
  “linkedin”: “secret-xxxxxx”
}
```

### Example of creating secret

```shell
kubectl create secret generic auth-credentials --from-file=jwt-public-key=app.rsa.pub \
    --from-file=jwt-private-key=app.rsa \
    --from-file=client-private-keys=client_secret.json
```


