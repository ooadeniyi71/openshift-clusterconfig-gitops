![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)

# setup-rbac-overview

GitOps wrapper for the [OpenShift Console RBAC Overview](https://github.com/tjungbauer/openshift-console-rbac-overview) dynamic plugin.

This chart does not duplicate the plugin manifests. It depends on the published Helm chart from the plugin repository:

- Chart source: `openshift-console-rbac-overview/chart/rbac-overview`
- Helm repository: `https://tjungbauer.github.io/openshift-console-rbac-overview`

Argo CD ApplicationSet discovers `config.json` under `clusters/management-cluster/**` and deploys this folder into the `rbac-overview` namespace on the management cluster.

## Values

Configure the upstream chart under the `rbac-overview:` key in `values.yaml` (image tag, `enableConsolePlugin`, `pluginConfig`, and so on).

## Refresh dependencies

After a new plugin chart release:

```bash
helm repo add rbac-overview https://tjungbauer.github.io/openshift-console-rbac-overview
helm repo update
helm dependency update clusters/management-cluster/setup-rbac-overview
```

Commit updated `Chart.lock` (and vendored `charts/*.tgz` if your pipeline requires them).
