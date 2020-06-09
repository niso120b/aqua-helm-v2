# Aqua CSP | Example

## Using local charts

please add comment to all `repository` in [Chart.yaml](../Chart.yaml)

```yaml
...
# repository: "http://helm.aquasec.com"
...
```

and then you need to add soft links for all components: *`server`*, *`gateway`* and *`database`*

```bash
ln -s $PWD/database $PWD/csp/charts/database
ln -s $PWD/gateway $PWD/csp/charts/gateway
ln -s $PWD/server $PWD/csp/charts/server
```

## Values file example

Steps:
* Create namespace
* Run helm command to deploy.

```bash
$ kubectl create ns aqua
$ helm install --namespace aqua <name> ./csp --set registry.username=<registry-username> --set registry.password=<registry-password>
```

> Note: each value that have prefix <name> in yaml its because the name of the deploy please update the example yaml

[**values.yaml**](../values.yaml)
```yaml
nameOverride: ""
fullnameOverride: ""

serviceAccount:
  # Specifies whether a service account should be created
  create: true
  # The name of the service account to use.
  # If not set and create is true, a name is generated using the fullname template
  name: aqua-sa
  # the image pull secrets list
  imagePullSecrets: []

registry:
  imagePullSecret:
    # Specifies whether a image pull secret should be created
    create: true
    # The name of the image pull secret to use.
    # If not set and create is true, a name is generated using the fullname template
    name: aqua-registry
  # aqua private registry
  name: registry.aquasec.com
  # aqua registry username
  username: "<Username for registry.aquasec.com>"
  # aqua registry password
  password: "<Password for registry.aquasec.com>"

database:
  enable: true
  serviceAccount:
    name: aqua-sa
    imagePullSecrets: 
    - aqua-registry
  
  service:
    type: ClusterIP

gateway:
  serviceAccount:
    name: aqua-sa
    imagePullSecrets: 
    - aqua-registry

  service:
    type: ClusterIP

  aqua:
    consoleSecureAddress: <name>-server:443
    db:
      host: <name>-database
      port: 5432
      passwordSecret:
        name: <name>-database-password
        key: password

server:
  serviceAccount:
    name: aqua-sa
    imagePullSecrets: 
    - aqua-registry

  service:
    type: LoadBalancer

  aqua:
    db:
      host: <name>-database
      port: 5432
      passwordSecret:
        name: <name>-database-password
        key: password
```