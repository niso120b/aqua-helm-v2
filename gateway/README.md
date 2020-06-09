# Aqua Security | Gateway Helm

Aqua gateway(s) handle communication between the Aqua Server and the Aqua Enforcer(s), and use the Aqua Database. The gateway(s) also interface the Aqua Server with any SIEM/Analytics systems you have integrated with Aqua CSP.
There must be at least one Aqua gateway instance in your environment. Multiple gateways can be deployed for redundancy and load balancing.

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
$ helm install --namespace <namespace> <name> ./gateway --set key=value[,key=value]
```

> note: recommended to use namespace aqua

## Configuration

Parameter | Description | Default
--------- | ----------- | -------
`replicaCount` | How many replicas to run. | `1`
`image.tag` | The image tag to use. | `5.0`
`image.registry` | The docker registry to use | `registry.aquasec.com`
`image.repository` | The docker image name to use. | `gateway`
`image.pullPolicy` | The kubernetes image pull policy. | `IfNotPresent`
`nameOverride` | Override the name of the chart. | `""`
`fullnameOverride` | Override the fullname of the chart. | `""`
`serviceAccount.create`| Specifies whether a ServiceAccount should be created | `false`
`serviceAccount.name` | The name of the ServiceAccount to use. | `nil`
`serviceAccount.imagePullSecrets` | Docker registry pull secret to add to the service account and to the deployment. | `[]`
`securityContext` | Set of security context for the container | `nil`
`service.type` | k8s service type | `ClusterIP`
`service.ssh.port` | External port for service | `3622`
`service.ssh.nodePort` | Port to use incase `service.type` set to `NodePort` | `nil`
`service.grpc.port` | External port for service | `8443`
`service.grpc.nodePort` | Port to use incase `service.type` set to `NodePort` | `nil`
`ingress.enabled` | If true, Ingress will be created | `false`
`ingress.annotations` | Ingress annotations | `[]`
`ingress.hosts` | Ingress hostnames | `[]`
`ingress.tls` | Ingress TLS configuration (YAML) | `[]`
`resources` | Resource requests and limits | `{}`
`nodeSelector` | Kubernetes node selector | `{}`
`tolerations` | Kubernetes node tolerations | `[]`
`affinity` | Kubernetes node affinity | `{}`
`aqua.consoleSecureAddress` | aqua console secure address for aqua server and gateway communication [link](https://docs.aquasec.com/docs/gateway-server-communication) | `nil`
`aqua.gatewayPublicIp` | the desired public IP address of the Aqua Gateway. Used to make the Enforcer connect to the Gateway through this IP address. | `nil`
`aqua.activeative` | set in active active mode. [link](https://docs.aquasec.com/docs/active-active-server-mode) | `false`
`aqua.db.host` | DNS name or IP address of the host of the Postgres configuration database | `nil`
`aqua.db.port` | Port of the Postgres configuration database. | `5432`
`aqua.db.user` | Username for connection to the Postgres configuration database. | `nil`
`aqua.db.scalockName` | Name of the Postgres configuration database name; all letters must be lower-case. | `nil`
`aqua.db.auditName` | Name of the Postgres Audit database; all letters must be lower-case. | `nil`
`aqua.db.pubsubName` | Name of the Postgres pubsub for active active database; all letters must be lower-case. | `nil`
`aqua.db.passwordSecret.name` | Password for connection to the PostgreSQL secret name | `nil`
`aqua.db.passwordSecret.key` | Password for connection to the PostgreSQL secret key | `nil`
`aqua.db.ssl` | If require an SSL-encrypted connection to the Postgres configuration database. | `true`

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

## Ingress

[Link](../docs/ingress.md)