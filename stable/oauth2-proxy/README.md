# oauth2-proxy

[oauth2-proxy](https://github.com/pusher/oauth2_proxy) is a reverse proxy and static file server that provides authentication using Providers (Google, GitHub, and others) to validate accounts by email, domain or group.

## TL;DR;

```console
$ helm install stable/oauth2-proxy
```

## Introduction

This chart bootstraps an oauth2-proxy deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install stable/oauth2-proxy --name my-release
```

The command deploys oauth2-proxy on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the oauth2-proxy chart and their default values.

Parameter | Description | Default
--- | --- | ---
`affinity` | node/pod affinities | None
`authenticatedEmailsFile.enabled` | Enables authorize individual email addresses | `false`
`authenticatedEmailsFile.template` | Name of the configmap what is handled outside of that chart | `""`
`authenticatedEmailsFile.restricted_access | (email addresses)[https://github.com/pusher/oauth2_proxy#email-authentication] list config | `""`
`config.clientID` | oauth client ID | `""`
`config.clientSecret` | oauth client secret | `""`
`config.cookieSecret` | server specific cookie for the secret; create a new one with `python -c 'import os,base64; print base64.b64encode(os.urandom(16))'` | `""`
`config.configFile` | custom [oauth2_proxy.cfg](https://github.com/pusher/oauth2_proxy/blob/master/contrib/oauth2_proxy.cfg.example) contents for settings not overridable via environment nor command line | `""`
`config.existingSecret` | existing Kubernetes secret to use for OAuth2 credentials. See [secret template](https://github.com/helm/charts/blob/master/stable/oauth2-proxy/templates/secret.yaml) for the required values | `nil`
`extraArgs` | key:value list of extra arguments to give the binary | `{}`
`image.pullPolicy` | Image pull policy | `IfNotPresent`
`image.repository` | Image repository | `quay.io/pusher/oauth2_proxy`
`image.tag` | Image tag | `v3.1.0`
`imagePullSecrets` | Specify image pull secrets | `nil` (does not add image pull secrets to deployed pods)
`ingress.enabled` | enable ingress | `false`
`nodeSelector` | node labels for pod assignment | `{}`
`podAnnotations` | annotations to add to each pod | `{}`
`podLabels` | additional labesl to add to each pod | `{}`
`replicaCount` | desired number of pods | `1`
`resources` | pod resource requests & limits | `{}`
`priorityClassName` | priorityClassName | `nil`
`service.port` | port for the service | `80`
`service.type` | type of service | `ClusterIP`
`tolerations` | List of node taints to tolerate | `[]`

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install stable/oauth2-proxy --name my-release \
  --set=image.tag=v0.0.2,resources.limits.cpu=200m
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install stable/oauth2-proxy --name my-release -f values.yaml
```

> **Tip**: You can use the default [values.yaml](values.yaml)
