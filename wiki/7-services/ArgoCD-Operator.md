# ArgoCD Operator

**Argo CD** is a declarative GitOps continuous delivery tool for Kubernetes. It can be managed as a service on Kubernetes via its own CRDs or the Argo CD Operator.

## Overview

Argo CD continuously monitors Git repositories and reconciles the live cluster state with the desired state defined in Git. See [CI CD](../4-kubernetes/CI-CD.md) for broader context on continuous delivery patterns.

## CRDs

| CRD | Purpose |
|---|---|
| `Application` | Maps a Git source (path, revision) to a target cluster/namespace |
| `ApplicationSet` | Template for generating multiple Applications (generators: Git, list, cluster, matrix, merge) |
| `AppProject` | RBAC boundary — restricts sources, destinations, and resource types |

## Key Features

- Git as single source of truth for application state
- Automatic or manual sync with drift detection
- Multi-cluster deployment
- SSO integration (OIDC, LDAP, SAML)
- Web UI, CLI, and API
- Health status and resource hooks
- ApplicationSet for multi-tenant and multi-cluster patterns

## Links

- [argo-cd.readthedocs.io](https://argo-cd.readthedocs.io/)
- [GitHub — argoproj/argo-cd](https://github.com/argoproj/argo-cd)
