# Aqua Security | CSP Helm

deployment of Aqua Cloud Native Security (CSP).

**CSP deployments include the following components:**

* Database *optional*
* Gateway
* Server

## Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)

## Prerequisites

- Kubernetes Cluster
- PV provisioner support in the underlying infrastructure
- Helm :)

## Installation

please view example [Link](docs/example.md)

## Configuration

Parameter | Description | Default
--------- | ----------- | -------
`nameOverride` | Override the name of the chart. | `""`
`fullnameOverride` | Override the fullname of the chart. | `""`
`serviceAccount.create`| Specifies whether a ServiceAccount should be created | `true`
`serviceAccount.name` | The name of the ServiceAccount to use. | `aqua-sa`
`serviceAccount.imagePullSecrets` | Docker registry pull secret to add to the service account and to the deployment. | `[]`
`registry.imagePullSecret.create` | Specifies whether a image pull secret should be created | `true`
`registry.imagePullSecret.name` | The name of the image pull secret to use. | `aqua-registry`
`registry.name` | aqua private registry | `registry.aquasec.com`
`registry.username` | aqua registry username | `nil`
`registry.password` | aqua registry password | `nil`
`database.enable` | if to install databse of using external | `true`
`database` | add the values you want to change from the defaults [link](../database/README.md#configuration) | **view in values file**
`gateway` | add the values you want to change from the defaults [link](../gateway/README.md#configuration) | **view in values file**
`server` | add the values you want to change from the defaults [link](../server/README.md#configuration) | **view in values file**

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.