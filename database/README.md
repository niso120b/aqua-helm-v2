# Aqua Security | Database Helm

PostgreSQL 9.6 image build by aqua security.

## Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Ingress](#ingress)
- [Persistence](#persistence)

## Prerequisites

- Kubernetes Cluster
- PV provisioner support in the underlying infrastructure
- Helm :)

## Installation

```bash
$ helm install --namespace <namespace> <name> ./database --set key=value[,key=value]
```

> note: recommended to use namespace aqua

## Configuration

Parameter | Description | Default
--------- | ----------- | -------
`replicaCount` | How many replicas to run. | `1`
`image.tag` | The image tag to use. | `5.0`
`image.registry` | The docker registry to use | `registry.aquasec.com`
`image.repository` | The docker image name to use. | `database`
`image.pullPolicy` | The kubernetes image pull policy. | `IfNotPresent`
`nameOverride` | Override the name of the chart. | `""`
`fullnameOverride` | Override the fullname of the chart. | `""`
`serviceAccount.create`| Specifies whether a ServiceAccount should be created | `false`
`serviceAccount.name` | The name of the ServiceAccount to use. | `nil`
`serviceAccount.imagePullSecrets` | Docker registry pull secret to add to the service account and to the deployment. | `[]`
`securityContext` | Set of security context for the container | `nil`
`service.type` | k8s service type | `ClusterIP`
`service.port` | External port for service | `5432`
`ingress.enabled` | If true, Ingress will be created | `false`
`ingress.annotations` | Ingress annotations | `[]`
`ingress.hosts` | Ingress hostnames | `[]`
`ingress.tls` | Ingress TLS configuration (YAML) | `[]`
`resources` | Resource requests and limits | `{}`
`nodeSelector` | Kubernetes node selector | `{}`
`tolerations` | Kubernetes node tolerations | `[]`
`affinity` | Kubernetes node affinity | `{}`
`persistence.enabled` | If true, Persistent Volume Claim will be created | `true`
`persistence.accessModes` | Persistent Volume access modes | `[ReadWriteOnce]`
`persistence.annotations` | Persistent Volume annotations | `{}`
`persistence.existingClaim` | Persistent Volume existing claim name | `""`
`persistence.size` | Persistent Volume size | `30Gi`
`persistence.storageClass` | Persistent Volume Storage Class |  `unset`

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

## Ingress

[Link](../docs/ingress.md)

## Persistence

The [PostgreSQL](https://hub.docker.com/_/postgres) image stores the PostgreSQL data and configurations at the `/var/lib/postgresql/data` path of the container.

[Link](../docs/storage.md)