# App Mesh Gateway

[App Mesh Gateway](https://github.com/stefanprodan/appmesh-gateway) Helm chart for Kubernetes

## Prerequisites

* Kubernetes >= 1.13
* App Mesh controller >= 0.2.0
* App Mesh inject >= 0.2.0

## Installing the Chart

Install App Mesh Gateway:

```sh
helm upgrade -i appmesh-gateway chart/appmesh-gateway \
--namespace appmesh-gateway \
--set mesh.name=global
```

Optionally you can create a mesh at install time:
  
```sh
helm upgrade -i appmesh-gateway chart/appmesh-gateway \
--namespace appmesh-system \
--set mesh.name=global \
--set mesh.create=true
```

The [configuration](#configuration) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `appmesh-gateway` deployment:

```console
helm delete --purge appmesh-gateway
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the chart and their default values.

Parameter | Description | Default
--- | --- | ---
`service.type` |  When set to LoadBalancer it creates an AWS NLB | `LoadBalancer`
`proxy.access_log_path` | to enable the access logs, set it to `/dev/stdout` | `/dev/null`
`proxy.image.repository` | image repository | `envoyproxy/envoy`
`proxy.image.tag` | image tag | `<VERSION>`
`proxy.image.pullPolicy` | image pull policy | `IfNotPresent`
`controller.image.repository` | image repository | `stefanprodan/appmesh-gateway`
`controller.image.tag` | image tag | `<VERSION>`
`controller.image.pullPolicy` | image pull policy | `IfNotPresent`
`resources.requests/cpu` | pod CPU request | `100m`
`resources.requests/memory` | pod memory request | `128Mi`
`resources.limits/memory` | pod memory limit | `2Gi`
`nodeSelector` | node labels for pod assignment | `{}`
`tolerations` | list of node taints to tolerate | `[]`
`rbac.create` | if `true`, create and use RBAC resources | `true`
`rbac.pspEnabled` | If `true`, create and use a restricted pod security policy | `false`
`serviceAccount.create` | If `true`, create a new service account | `true`
`serviceAccount.name` | Service account to be used | None
`mesh.create` | If `true`, create mesh custom resource | `false`
`mesh.name` | The name of the mesh to use | `global`
`mesh.discovery` | The service discovery type to use, can be dns or cloudmap | `dns`

