# CNOE Technology Choices

Every organization's Internal Developer Platform (IDP) differs, but common tooling and patterns emerge. CNOE captures community-driven references for tools commonly deployed in production, how they are configured, and how they combine.

This page complements the ApeiroRA [[Apeiro-Reference-Architecture]] by mapping CNOE-endorsed technologies to platform capabilities.

## Capability-to-Technology Map

| Capability | CNOE Technologies | ApeiroRA Relation |
|---|---|---|
| Code Repository | Git | Foundation for [[GitOps-and-Repositories]] |
| Config Repository | Git | Key-value, hierarchical, versioned config -- see [[GitOps-and-Repositories]] |
| Artifact Registry | Container Registries (OCI) | [[Software-Bill-of-Delivery]] (OCM uses OCI) |
| Secret Repository | External Secrets (with Vault, KMS) | [[Secrets-Management]], [[Key-Management]] |
| Validations | CNOE Validators | [[Validation-and-Policy]] |
| Secret Management | External Secrets Operator | [[Secrets-Management]] |
| Infrastructure as Code | Terraform, Crossplane | [[Infrastructure-as-Code]], [[KRM]] (Crossplane is KRM-based) |
| Continuous Delivery | ArgoCD, Flux | [[CI-CD]], [[Controller-Pattern]] (reconciling controllers) |
| Continuous Integration | Argo Workflows, Tekton | [[CI-CD]] |
| Identity and Access | Keycloak | [[Platform-Mesh-Security]], [[Security]] |
| Developer Portals | Backstage | [[Developer-Portal]], [[OpenMFP]] |

## Design Principles Behind Choices

- **Open source first** -- All technologies listed are OSS, aligned with the CNOE tenet that open source is prioritized over proprietary alternatives.
- **Pluggability** -- Within each capability category, multiple tools are endorsed. Any CI tool works with any CD tool. This reduces lock-in while maintaining interoperability.
- **Kubernetes-native** -- All tools run on Kubernetes. Crossplane and ArgoCD use the [[Controller-Pattern]] for continuous reconciliation. Terraform integrates via controllers like the Terraform Controller.
- **Community consensus** -- Selections reflect what large enterprises actually deploy, not theoretical best picks.

## Relation to Apeiro

Apeiro's [[Platform-Mesh]] extends beyond CNOE's scope by adding multi-cloud service-provider control planes ([[Service-Provider-Control-Planes]]), data fabric ([[Data-Fabric]]), and the [[Konfidence]] lifecycle management layer. CNOE tools slot into the Kubernetes and platform-mesh layers of the 7-layer architecture.

Where CNOE uses Backstage for developer portals, Apeiro uses [[OpenMFP]] as its micro-frontend platform, potentially hosting Backstage plugins within the broader [[Micro-Frontends]] framework.

## See Also

- [[CNOE]] -- Overview, tenets, personas
- [[IDP-Reference-Implementation]] -- Reference deployment using these technologies
