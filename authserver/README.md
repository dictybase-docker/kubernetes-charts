# authserver
This [helm](https://github.com/kubernetes/helm) chart provides
[kubernetes](http://kubernetes.io) manifests for running
[authserver](https://github.com/dictyBase/authserver).

## Credentials
The manifests for [secrets](http://kubernetes.io/docs/user-guide/secrets/) are
in the `sample` file. Copy the file `_sample_pre-install.yaml` to
`credentials.yaml` and then fill up the appropiate secret keys. Any file name
with `credentials` are ignored in this chart repo by default and will not be
pushed to any remote.

### Secret keys
All values have to be `base64` encoded.

* jwt-public-key
* jwt-private-key
* oauth-secret-key : This one should be a json string in the following format.

```json
{
  “google”: “secret-xxxxxxx”,
  “linkedin”: “secret-xxxxxx”
}
```

It’s preferable to save it in a file and then encode with `base64`
```
base64 -w 0 [file]
```
