# Aqua Security | Server Helm

The Aqua Consoles page of the UI lists the Aqua consoles (Servers) deployed in your environment, and provides basic status information on the consoles.

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
`image.repository` | The docker image name to use. | `server`
`image.pullPolicy` | The kubernetes image pull policy. | `IfNotPresent`
`nameOverride` | Override the name of the chart. | `""`
`fullnameOverride` | Override the fullname of the chart. | `""`
`serviceAccount.create`| Specifies whether a ServiceAccount should be created | `false`
`serviceAccount.name` | The name of the ServiceAccount to use. | `nil`
`serviceAccount.imagePullSecrets` | Docker registry pull secret to add to the service account and to the deployment. | `[]`
`securityContext` | Set of security context for the container | `nil`
`service.type` | k8s service type | `ClusterIP`
`service.web.port` | External port for service | `8080`
`service.web.nodePort` | Port to use incase `service.type` set to `NodePort` | `nil`
`service.grpc.port` | External port for service | `443`
`service.grpc.nodePort` | Port to use incase `service.type` set to `NodePort` | `nil`
`ingress.enabled` | If true, Ingress will be created | `false`
`ingress.annotations` | Ingress annotations | `[]`
`ingress.hosts` | Ingress hostnames | `[]`
`ingress.tls` | Ingress TLS configuration (YAML) | `[]`
`resources` | Resource requests and limits | `{}`
`nodeSelector` | Kubernetes node selector | `{}`
`tolerations` | Kubernetes node tolerations | `[]`
`affinity` | Kubernetes node affinity | `{}`
`aqua.adminPassword` | Set up the password of the Aqua Server user administrator. | `nil`
`aqua.licenseToken` | License string received from Aqua Security to activate full use of the software. | `nil`
`aqua.dockerless` | Scanning mode direct or docker [link](https://docs.aquasec.com/docs/scanning-mode#default-scanning-mode) | `true`
`aqua.activeative` | set in active active mode. [link](https://docs.aquasec.com/docs/active-active-server-mode) | `false`
`aqua.encryptionKey` | Encryption key that will be used by Aqua Server and Aqua Gateway to encrypt sensitive data in the Aqua database. | `nil`
`aqua.httpProxy` | URL of HTTP proxy, if used. | `nil`
`aqua.httpsProxy` | URL of HTTPS proxy, if used. | `nil`
`aqua.noProxy` | List of addresses that bypass the proxy. Specify the URLs of internal private registries, if used. | `nil`
`aqua.dockerSocketPath` | docker socket path | `/var/run/docker.sock`
`aqua.db.host` | DNS name or IP address of the host of the Postgres configuration database | `nil`
`aqua.db.port` | Port of the Postgres configuration database. | `5432`
`aqua.db.user` | Username for connection to the Postgres configuration database. | `nil`
`aqua.db.scalockName` | Name of the Postgres configuration database name; all letters must be lower-case. | `nil`
`aqua.db.auditName` | Name of the Postgres Audit database; all letters must be lower-case. | `nil`
`aqua.db.pubsubName` | Name of the Postgres pubsub for active active database; all letters must be lower-case. | `nil`
`aqua.db.passwordSecret.name` | Password for connection to the PostgreSQL secret name | `nil`
`aqua.db.passwordSecret.key` | Password for connection to the PostgreSQL secret key | `nil`
`aqua.db.ssl` | If require an SSL-encrypted connection to the Postgres configuration database. | `true`
`persistence.enabled` | If true, Persistent Volume Claim will be created | `true`
`persistence.accessModes` | Persistent Volume access modes | `[ReadWriteOnce]`
`persistence.annotations` | Persistent Volume annotations | `{}`
`persistence.existingClaim` | Persistent Volume existing claim name | `""`
`persistence.size` | Persistent Volume size | `10Gi`
`persistence.storageClass` | Persistent Volume Storage Class |  `unset`


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

## Ingress

[Link](../docs/ingress.md)

## Persistence

[Link](../docs/storage.md)