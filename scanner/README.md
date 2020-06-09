# Aqua Security | Scanner Helm

The scanner can operate in either of two modes:
* **Direct scanning mode** (previously called "scanning without a Docker socket"): The scanner pulls the image directly from a registry, and scans it as a file.
* **Docker scanning mode** The scanner is mounted to the local Docker service (docker.sock) to pull the image, and scans it as a running container. This mode is supported only if the container engine is Docker.

## Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)

## Prerequisites

- Kubernetes Cluster
- PV provisioner support in the underlying infrastructure
- Helm :)

## Installation

```bash
$ helm install --namespace <namespace> <name> ./scanner --set key=value[,key=value]
```

> note: recommended to use namespace aqua

## Configuration

Parameter | Description | Default
--------- | ----------- | -------
`replicaCount` | How many replicas to run. | `1`
`image.tag` | The image tag to use. | `5.0`
`image.registry` | The docker registry to use | `registry.aquasec.com`
`image.repository` | The docker image name to use. | `scanner`
`image.pullPolicy` | The kubernetes image pull policy. | `IfNotPresent`
`nameOverride` | Override the name of the chart. | `""`
`fullnameOverride` | Override the fullname of the chart. | `""`
`serviceAccount.create`| Specifies whether a ServiceAccount should be created | `false`
`serviceAccount.name` | The name of the ServiceAccount to use. | `nil`
`serviceAccount.imagePullSecrets` | Docker registry pull secret to add to the service account and to the deployment. | `[]`
`securityContext` | Set of security context for the container | `nil`
`resources` | Resource requests and limits | `{}`
`nodeSelector` | Kubernetes node selector | `{}`
`tolerations` | Kubernetes node tolerations | `[]`
`affinity` | Kubernetes node affinity | `{}`
`aqua.user` | aqua username | `administrator`
`aqua.password` | aqua user password | `nil`
`aqua.host` | aqua host | `nil`
`aqua.dockerless` | Scanning mode direct or docker [Link](https://docs.aquasec.com/docs/scanning-mode#default-scanning-mode) | `true`
`aqua.dockerSocketPath` | docker socket path for example for pks - /var/vcap/data/sys/run/docker/docker.sock | `/var/run/docker.sock`


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.