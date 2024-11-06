# Redpanda Connect Chart Specification
---
description: Find the default values and descriptions of settings in the Redpanda Connect Helm chart.
---

![Version: 3.0.1](https://img.shields.io/badge/Version-3.0.1-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 4.39.0](https://img.shields.io/badge/AppVersion-4.39.0-informational?style=flat-square)

Redpanda Connect is a high performance and resilient stream processor, able to connect various sources and sinks in a range of brokering patterns and perform hydration, enrichments, transformations and filters on payloads.

This Helm Chart deploys a single Redpanda Connect instance in either streams mode or standalone.

This page describes the official Redpanda Connect Helm Chart. In particular, this page describes the contents of the chart’s [`values.yaml` file](https://github.com/redpanda-data/helm-charts/blob/main/charts/connect/values.yaml). Each of the settings is listed and described on this page, along with any default values.

For instructions on how to install and use the chart, including how to override and customize the chart’s values, refer to the [deployment documentation](https://docs.redpanda.com/docs/deploy/deployment-option/self-hosted/kubernetes/kubernetes-deploy/).

### Migration from Benthos

If you are coming here from [the old Benthos based chart](https://github.com/redpanda-data/redpanda-connect-helm-chart), please see the [migration guide in this repo](https://github.com/redpanda-data/helm-charts/blob/main/charts/connect/MIGRATION_FROM_BENTHOS.md).

### Streams mode

When running Redpanda Connect in [streams mode](https://docs.redpanda.com/redpanda-connect/guides/streams_mode/about/), all individual stream configuration files should be combined and placed in a single Kubernetes `ConfigMap`, like so:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: connect-streams
data:
  hello.yaml: |
    input:
      generate:
        mapping: root = "woof"
        interval: 5s
        count: 0
    output:
      stdout:
        codec: lines
  aaaaa.yaml: |
    input:
      generate:
        mapping: root = "meow"
        interval: 2s
        count: 0
    output:
      stdout:
        codec: lines
```

Then you can simply reference your `ConfigMap` and enable streams mode in your `values.yaml` file.
```yaml
# values.yaml
streams:
  enabled: true
  streamsConfigMap: "connect-streams"
```

Currently the streams mode `ConfigMap` should be applied **separately from and before installation of** the helm chart; support for deploying additional `ConfigMap`'s within the chart may be implemented later.

### Global Configuration

When deploying Redpanda Connect in streams mode, you may want to configure global tracing, logging and http configuration which is shared across all of your pipelines.

This can be done by specifying configuration under the `metrics`, `logger` and `tracing` configuration sections in your `values.yaml` file. These all use their respective upstream Redpanda Connect configuration syntax.

```yaml
metrics:
  prometheus: {}

tracing:
  openTelemetry:
    http: []
    grpc: []
    tags: {}

logger:
  level: INFO
  static_fields:
    '@service': redpanda-connect
```

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.13.1](https://github.com/norwoodj/helm-docs/releases/v1.13.1)

## Source Code

* <https://github.com/redpanda-data/helm-charts>

## Settings

### [affinity](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=affinity)

**Default:** `{}`

### [args](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=args)

Override Redpanda Connect's default arguments passed with command.

**Default:** `[]`

### [autoscaling.enabled](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=autoscaling.enabled)

**Default:** `false`

### [autoscaling.maxReplicas](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=autoscaling.maxReplicas)

**Default:** `12`

### [autoscaling.metrics[0].resource.name](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=autoscaling.metrics[0].resource.name)

**Default:** `"cpu"`

### [autoscaling.metrics[0].resource.target.averageUtilization](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=autoscaling.metrics[0].resource.target.averageUtilization)

**Default:** `80`

### [autoscaling.metrics[0].resource.target.type](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=autoscaling.metrics[0].resource.target.type)

**Default:** `"Utilization"`

### [autoscaling.metrics[0].type](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=autoscaling.metrics[0].type)

**Default:** `"Resource"`

### [autoscaling.minReplicas](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=autoscaling.minReplicas)

**Default:** `1`

### [command](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=command)

Command replaces the entrypoint command of the docker

**Default:** `[]`

### [commonLabels](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=commonLabels)

Add additional labels to all created resources.

**Default:** `{}`

### [config](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=config)

**Default:** `{}`

### [deployment.annotations](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.annotations)

**Default:** `{}`

### [deployment.livenessProbe.failureThreshold](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.livenessProbe.failureThreshold)

**Default:** `3`

### [deployment.livenessProbe.httpGet.path](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.livenessProbe.httpGet.path)

**Default:** `"/ping"`

### [deployment.livenessProbe.httpGet.port](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.livenessProbe.httpGet.port)

**Default:** `"http"`

### [deployment.livenessProbe.periodSeconds](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.livenessProbe.periodSeconds)

**Default:** `5`

### [deployment.livenessProbe.successThreshold](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.livenessProbe.successThreshold)

**Default:** `1`

### [deployment.livenessProbe.timeoutSeconds](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.livenessProbe.timeoutSeconds)

**Default:** `2`

### [deployment.podAnnotations](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.podAnnotations)

**Default:** `{}`

### [deployment.podLabels](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.podLabels)

**Default:** `{}`

### [deployment.readinessProbe.failureThreshold](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.readinessProbe.failureThreshold)

**Default:** `1`

### [deployment.readinessProbe.httpGet.path](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.readinessProbe.httpGet.path)

**Default:** `"/ready"`

### [deployment.readinessProbe.httpGet.port](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.readinessProbe.httpGet.port)

**Default:** `"http"`

### [deployment.readinessProbe.periodSeconds](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.readinessProbe.periodSeconds)

**Default:** `5`

### [deployment.readinessProbe.successThreshold](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.readinessProbe.successThreshold)

**Default:** `1`

### [deployment.readinessProbe.timeoutSeconds](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.readinessProbe.timeoutSeconds)

**Default:** `2`

### [deployment.replicaCount](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.replicaCount)

**Default:** `1`

### [deployment.restartPolicy](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.restartPolicy)

**Default:** `"Always"`

### [deployment.rolloutConfigMap](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.rolloutConfigMap)

**Default:** `true`

### [deployment.terminationGracePeriodSeconds](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=deployment.terminationGracePeriodSeconds)

**Default:** `60`

### [env](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=env)

**Default:** `[]`

### [envFrom](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=envFrom)

Define environment variables from Secrets or ConfigMaps. https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/#define-an-environment-variable-for-a-container

**Default:** `[]`

### [extraVolumeMounts](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=extraVolumeMounts)

**Default:** `[]`

### [extraVolumes](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=extraVolumes)

**Default:** `[]`

### [fullnameOverride](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=fullnameOverride)

**Default:** `""`

### [http.address](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=http.address)

**Default:** `"0.0.0.0:4195"`

### [http.cors.enabled](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=http.cors.enabled)

**Default:** `false`

### [http.debug_endpoints](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=http.debug_endpoints)

**Default:** `false`

### [http.enabled](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=http.enabled)

**Default:** `true`

### [http.root_path](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=http.root_path)

**Default:** `"/redpanda-connect"`

### [image.pullPolicy](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=image.pullPolicy)

**Default:** `"IfNotPresent"`

### [image.repository](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=image.repository)

**Default:**

```
"docker.redpanda.com/redpandadata/connect"
```

### [image.tag](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=image.tag)

**Default:** `""`

### [imagePullSecrets](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=imagePullSecrets)

**Default:** `[]`

### [ingress.annotations](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=ingress.annotations)

**Default:** `{}`

### [ingress.className](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=ingress.className)

**Default:** `""`

### [ingress.enabled](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=ingress.enabled)

**Default:** `false`

### [ingress.hosts](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=ingress.hosts)

**Default:** `[]`

### [ingress.tls](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=ingress.tls)

**Default:** `[]`

### [initContainers](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=initContainers)

Init Containers to be added to the Redpanda Connect Pods.

**Default:** `[]`

### [nameOverride](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=nameOverride)

**Default:** `""`

### [nodeSelector](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=nodeSelector)

**Default:** `{}`

### [podDisruptionBudget.enabled](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=podDisruptionBudget.enabled)

Enable a [PodDisruptionBudget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) for Redpanda Connect.

**Default:** `false`

### [podSecurityContext](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=podSecurityContext)

**Default:** `{}`

### [resources](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=resources)

**Default:** `{}`

### [securityContext](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=securityContext)

**Default:** `{}`

### [service.extraPorts](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=service.extraPorts)

**Default:** `nil`

### [service.name](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=service.name)

**Default:** `"http"`

### [service.port](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=service.port)

**Default:** `80`

### [service.protocol](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=service.protocol)

**Default:** `"TCP"`

### [service.targetPort](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=service.targetPort)

**Default:** `"http"`

### [service.type](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=service.type)

**Default:** `"ClusterIP"`

### [serviceAccount.annotations](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=serviceAccount.annotations)

**Default:** `{}`

### [serviceAccount.create](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=serviceAccount.create)

**Default:** `true`

### [serviceAccount.name](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=serviceAccount.name)

**Default:** `""`

### [serviceMonitor.enabled](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=serviceMonitor.enabled)

**Default:** `false`

### [serviceMonitor.interval](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=serviceMonitor.interval)

**Default:** `"10s"`

### [serviceMonitor.scheme](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=serviceMonitor.scheme)

**Default:** `"http"`

### [streams.api.enable](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=streams.api.enable)

**Default:** `true`

### [streams.enabled](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=streams.enabled)

**Default:** `false`

### [streams.streamsConfigMap](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=streams.streamsConfigMap)

**Default:** `""`

### [telemetry](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=telemetry)

**Default:** `true`

### [tolerations](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=tolerations)

**Default:** `[]`

### [topologySpreadConstraints](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=topologySpreadConstraints)

**Default:** `[]`

### [updateStrategy](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=updateStrategy)

**Default:** `{}`

### [watch](https://artifacthub.io/packages/helm/redpanda-data/redpanda?modal=values&path=watch)

**Default:** `false`
