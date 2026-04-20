# IDP Reference Implementation

The CNOE IDP Reference Implementation is a deployable stack that demonstrates how CNOE-endorsed technologies work together as an Internal Developer Platform. It uses the **IDPBuilder** tool to stand up the full stack locally or in cloud environments. This page covers the CNOE reference approach; for ApeiroRA's equivalent demonstration concepts, see [[Showroom-Scenarios]].

## IDPBuilder

IDPBuilder is a CLI tool that spins up a complete IDP on a local machine or in Codespaces. It requires only Docker as a local dependency.

**What IDPBuilder creates:**
1. A local Kind cluster (Kubernetes-in-Docker)
2. Self-signed TLS certificates for ingress
3. CoreDNS configuration for in-cluster name resolution
4. Core packages managed via ArgoCD and GitOps:
   - **ArgoCD** -- GitOps CD, manages all other packages
   - **Gitea** -- In-cluster Git server with OCI container registry
   - **Ingress-nginx** -- Ingress controller for routing

Once core packages are installed, IDPBuilder hands control to ArgoCD. From that point, ArgoCD manages everything through manifests in Gitea repositories -- GitOps all the way down.

## What Gets Installed (Reference Stack)

The full reference implementation adds these packages on top of the core:

| Component | Role |
|-----------|------|
| **ArgoCD** | GitOps continuous delivery ([[CI-CD]]) |
| **Argo Workflows** | Workflow orchestration for CI pipelines ([[CI-CD]]) |
| **Backstage** | Developer portal -- software catalog, templates ([[Developer-Portal]]) |
| **Crossplane** | Infrastructure as Code with AWS providers ([[Infrastructure-as-Code]]) |
| **External Secrets** | Secret generation and coordination ([[Secrets-Management]]) |
| **Keycloak** | Identity provider, SSO for all components |
| **Spark Operator** | Example workload demonstrating Spark job integration |

Packages are modular -- any can be removed by deleting its ArgoCD Application manifest (except Keycloak, which others depend on).

## Use Cases

### Basic Deployment
Create a deployment through Backstage templates:
1. Backstage creates a Git repo in Gitea with templated contents
2. Backstage creates an ArgoCD Application pointing to that repo
3. Backstage registers the component in the software catalog
4. ArgoCD deploys manifests from the repo to the cluster

### Workflow Orchestration
Argo Workflows runs Spark jobs orchestrated through Backstage:
1. Backstage template creates a workflow definition
2. ArgoCD deploys the workflow to the cluster
3. Argo Workflows executes the Spark job
4. Status visible in both Argo Workflows UI and Backstage entity page

### Cloud Resources
Crossplane provisions cloud infrastructure (e.g., S3 buckets) through the same GitOps pattern:
1. Backstage template creates a Crossplane claim
2. ArgoCD syncs the claim to the cluster
3. Crossplane reconciles the claim to AWS APIs
4. Compositions enforce security requirements (encryption, tagging)

## Architecture Pattern

```
Developer --> Backstage --> Gitea (Git repo) --> ArgoCD --> Cluster
                              |                    |
                              |                    +--> Crossplane --> Cloud APIs
                              |
                              +--> ArgoCD Application (auto-created)
```

All interactions flow through Git. Backstage is the UI layer; ArgoCD is the reconciliation engine. This demonstrates the [[GitOps-and-Repositories]] pattern end to end.

## Relation to ApeiroRA Showroom

The CNOE reference implementation and ApeiroRA [[Showroom-Scenarios]] serve similar purposes -- demonstrating platform capabilities through deployable stacks. Key differences:

- **CNOE ref impl** focuses on the developer platform toolchain (CI/CD, portal, IaC)
- **ApeiroRA showroom** demonstrates the full 7-layer architecture including [[Data-Fabric]], [[Konfidence]] lifecycle management, and [[Platform-Mesh]] multi-cloud capabilities
- Both use Kubernetes as the foundation and GitOps for configuration management

## Getting Started

```bash
idpbuilder create --use-path-routing \
  --package https://github.com/cnoe-io/stacks//ref-implementation
```

Access UIs at `https://cnoe.localtest.me:8443/` (Backstage, ArgoCD, Argo Workflows, Gitea, Keycloak).

## See Also

- [[Showroom-Scenarios]] -- ApeiroRA demonstration scenarios
- [[CNOE-Technology-Choices]] -- Full technology mapping
- [[CI-CD]] -- ArgoCD and Argo Workflows details
- [[Developer-Portal]] -- Backstage details
- [[Infrastructure-as-Code]] -- Crossplane details
- [[CNOE]] -- Framework overview

## Deep Dive

- [[IDPBuilder-Details]] -- Networking, certificates, OCI registry, Gitea integration
- [[IDPBuilder-Stacks]] -- Available community stacks (Localstack, Dapr, Kyverno, Istio, etc.)
- [[Backstage-Plugins]] -- CNOE-developed Backstage plugins
- [[CNOE-CLI]] -- Template generation and verification tools
