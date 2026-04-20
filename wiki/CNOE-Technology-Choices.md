# CNOE Technology Choices

Every organization's Internal Developer Platform (IDP) differs, but common tooling and patterns emerge. CNOE captures community-driven references for tools commonly deployed in production, how they are configured, and how they combine.

This page complements the ApeiroRA [Apeiro Reference Architecture](Apeiro-Reference-Architecture.md) by mapping CNOE-endorsed technologies to platform capabilities.

## Capability-to-Technology Map

| Capability | CNOE Technologies | ApeiroRA Relation |
|---|---|---|
| Code Repository | Git | Foundation for [GitOps and Repositories](4-kubernetes/GitOps-and-Repositories.md) |
| Config Repository | Git | Key-value, hierarchical, versioned config -- see [GitOps and Repositories](4-kubernetes/GitOps-and-Repositories.md) |
| Artifact Registry | Container Registries (OCI) | [Software Bill of Delivery](5-software-delivery/Software-Bill-of-Delivery.md) (OCM uses OCI) |
| Secret Repository | External Secrets (with Vault, KMS) | [Secrets Management](8-platform-mesh/Secrets-Management.md), [Key Management](8-platform-mesh/Key-Management.md) |
| Validations | CNOE Validators | [Validation and Policy](4-kubernetes/Validation-and-Policy.md) |
| Secret Management | External Secrets Operator | [Secrets Management](8-platform-mesh/Secrets-Management.md) |
| Infrastructure as Code | Terraform, Crossplane | [Infrastructure as Code](4-kubernetes/Infrastructure-as-Code.md), [KRM](4-kubernetes/KRM.md) (Crossplane is KRM-based) |
| Continuous Delivery | ArgoCD, Flux | [CI CD](4-kubernetes/CI-CD.md), [Controller Pattern](4-kubernetes/Controller-Pattern.md) (reconciling controllers) |
| Continuous Integration | Argo Workflows, Tekton | [CI CD](4-kubernetes/CI-CD.md) |
| Identity and Access | Keycloak | [Platform Mesh Security](8-platform-mesh/Platform-Mesh-Security.md), [Security](8-platform-mesh/Security.md) |
| Developer Portals | Backstage | [Developer Portal](10-portals/Developer-Portal.md), [OpenMFP](5-software-delivery/OpenMFP.md) |

## Design Principles Behind Choices

- **Open source first** -- All technologies listed are OSS, aligned with the CNOE tenet that open source is prioritized over proprietary alternatives.
- **Pluggability** -- Within each capability category, multiple tools are endorsed. Any CI tool works with any CD tool. This reduces lock-in while maintaining interoperability.
- **Kubernetes-native** -- All tools run on Kubernetes. Crossplane and ArgoCD use the [Controller Pattern](4-kubernetes/Controller-Pattern.md) for continuous reconciliation. Terraform integrates via controllers like the Terraform Controller.
- **Community consensus** -- Selections reflect what large enterprises actually deploy, not theoretical best picks.

## Relation to Apeiro

Apeiro's [Platform Mesh](8-platform-mesh/Platform-Mesh.md) extends beyond CNOE's scope by adding multi-cloud service-provider control planes ([Service Provider Control Planes](8-platform-mesh/Service-Provider-Control-Planes.md)), data fabric ([Data Fabric](6-data-fabric/Data-Fabric.md)), and the [Konfidence](5-software-delivery/Konfidence.md) lifecycle management layer. CNOE tools slot into the Kubernetes and platform-mesh layers of the 7-layer architecture.

Where CNOE uses Backstage for developer portals, Apeiro uses [OpenMFP](5-software-delivery/OpenMFP.md) as its micro-frontend platform, potentially hosting Backstage plugins within the broader [Micro Frontends](5-software-delivery/Micro-Frontends.md) framework.

## See Also

- [CNOE](CNOE.md) -- Overview, tenets, personas
- [IDP Reference Implementation](10-portals/IDP-Reference-Implementation.md) -- Reference deployment using these technologies
