# Aqua Security | Enforcer Helm

**Aqua Enforcers provide runtime protection for:**

* Containers
* Hosts (virtual machines) with either Docker or Kubernetes.

It is required that you deploy an Enforcer (as a container) on each host for which you want to monitor, protect, and audit the runtime activity of containers and the host itself.

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
$ helm install --namespace <namespace> <name> ./enforcer --set key=value[,key=value]
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
`securityContext.privileged` | determines if any container in a pod can enable privileged mode. | `true`
`securityContext.capabilities` | Linux capabilities provide a finer grained breakdown of the privileges traditionally associated with the superuser. | `unset`
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
`aqua.gateway` | gateway address and port. Do not provide the scheme (e.g., https://) | `nil`
`aqua.networkControl` | Specify false if you would like the Aqua Enforcer to be deployed without modifying the host's iptable. | `true`
`aqua.hostRunPath` | for changing host run path for example for **pks** need to change to `/var/vcap/sys/run/docker` | `nil`
`aqua.restartContainers` | Specify true for making the Enforcer restart all containers that were running before Aqua was deployed. | `false`
`aqua.runcInterception` | Specify the *interception mode* for the Enforcer: `false` for docker, `true` for runc | `false`
`aqua.token` | Specify the installation token retrieved from the Aqua Server. | `nil`
`aqua.tokenSecret.name` | token secret name | `nil`
`aqua.tokenSecret.key` | token secret key | `nil`

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

## Privileged

determines if any container in a pod can enable privileged mode. By default a container is not allowed to access any devices on the host, but a `privileged` container is given access to all devices on the host. This allows the container nearly all the same access as processes running on the host. This is useful for containers that want to use linux capabilities like manipulating the network stack and accessing devices.

for more information, [link](https://kubernetes.io/docs/concepts/policy/pod-security-policy/#privileged)

### Capabilities

Linux capabilities provide a finer grained breakdown of the privileges traditionally associated with the superuser. Some of these capabilities can be used to escalate privileges or for container breakout, and may be restricted by the `PodSecurityPolicy`.
The following fields take a list of capabilities, specified as the capability name in ALL_CAPS without the CAP_ prefix.

for more information, [link](https://kubernetes.io/docs/concepts/policy/pod-security-policy/#capabilities)