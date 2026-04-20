# IDPBuilder Stacks

A Stack is a collection of packages (ArgoCD applications) that define "what" gets installed in an IDP, while IDPBuilder handles "how" to install it. Each stack can contain any number of packages, using either local files (via the `cnoe://` scheme pushed to Gitea) or remote references (Helm charts, external repos).

Anyone can create custom stacks and publish them in the [stacks repository](https://github.com/cnoe-io/stacks).

## Installing a Stack

Use the `-p` flag to specify package directories (local or remote). Remote directories must use [kustomize remote URL format](https://github.com/kubernetes-sigs/kustomize/blob/master/examples/remoteBuild.md).

```bash
# Remote
idpbuilder create \
  -p https://github.com/cnoe-io/stacks//basic/package1 \
  -p https://github.com/cnoe-io/stacks//basic/package2

# Local
git clone https://github.com/cnoe-io/stacks.git
idpbuilder create \
  -p stacks/basic/package1 \
  -p stacks/basic/package2
```

## Available Stacks

| Stack | Maintainer | Description |
|-------|-----------|-------------|
| **Localstack** | CNOE | Local AWS emulation integrated with Crossplane. [stacks/localstack-integration](https://github.com/cnoe-io/stacks/tree/main/localstack-integration) |
| **Local Backup** | CNOE | Backs up Kubernetes objects to the local machine. [stacks/local-backup](https://github.com/cnoe-io/stacks/blob/main/local-backup) |
| **Terraform Integrations** | CNOE | FluxCD source controller + tofu-controller for Terraform lifecycle management from Kubernetes. [stacks/terraform-integrations](https://github.com/cnoe-io/stacks/tree/main/terraform-integrations) |
| **Dapr Integrations** | CNOE | Dapr control plane with Redis-backed state store and pub/sub. [stacks/dapr-integration](https://github.com/cnoe-io/stacks/tree/main/dapr-integration) |
| **Crossplane Integrations** | CNOE | Deploy apps with Crossplane-managed cloud resources via Backstage templates. [stacks/crossplane-integrations](https://github.com/cnoe-io/stacks/tree/main/crossplane-integrations) |
| **Istio Ambient** | Community | Istio Ambient mesh with observability tools for traffic, metrics, and traces. [stacks/istio-ambient](https://github.com/cnoe-io/stacks/tree/main/istio-ambient) |
| **JupyterHub** | Community | JupyterHub with Keycloak SSO authentication. [stacks/jupyterhub](https://github.com/cnoe-io/stacks/tree/main/jupyterhub) |
| **Kyverno** | Community | Kubernetes-native policy engine for enforcement and audit. [stacks/kyverno-integration](https://github.com/cnoe-io/stacks/tree/main/kyverno-integration) |
| **vcluster Multi-Env** | Community | Multi-environment emulation with virtual clusters (staging, production) enrolled in ArgoCD. [stacks/vcluster-multi-env](https://github.com/cnoe-io/stacks/tree/main/vcluster-multi-env) |

## Stack Anatomy

Each package directory contains ArgoCD Application or ApplicationSet files. The `cnoe://` prefix in `repoURL` triggers local sync:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
spec:
  source:
    repoURL: cnoe://manifests
```

IDPBuilder then: (1) creates a Gitea repository, (2) pushes the local manifests into it, (3) updates the Application to point at the Gitea repo. ArgoCD takes over from there.

## See Also

- [IDP Reference Implementation](IDP-Reference-Implementation.md) -- Full reference stack deployment
- [CNOE](../CNOE.md) -- Framework overview
