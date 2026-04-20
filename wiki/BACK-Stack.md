# BACK Stack

Website: [backstack.dev](https://backstack.dev/)

## What Is the BACK Stack?

The BACK Stack is a reference architecture for building an Internal Developer Platform (IDP) using four CNCF projects:

| Letter | Project | Role | ApeiroRA equivalent |
|---|---|---|---|
| **B** | Backstage | Developer portal — service catalog, golden paths, docs | [[Developer-Portal]] |
| **A** | Argo CD | GitOps continuous delivery | [[CI-CD]] |
| **C** | Crossplane | Infrastructure-as-Code via Kubernetes API (compositions, XRDs) | [[Infrastructure-as-Code]] |
| **K** | Kyverno | Policy engine — validation, mutation, generation of resources | [[Validation-and-Policy]] |

Together these four components provide:

- **Service catalog and developer self-service** (Backstage)
- **Declarative, GitOps-driven deployment** (Argo CD)
- **Cloud resource provisioning as Kubernetes resources** (Crossplane)
- **Policy enforcement and guardrails** (Kyverno)

## How It Works

1. Developer creates a service from a **Backstage template** (golden path)
2. Template generates a Git repo with application code + Crossplane compositions
3. **Argo CD** syncs the repo to the cluster, deploying both app and infrastructure
4. **Kyverno** policies validate and mutate resources at admission time (security, labeling, resource limits)
5. **Crossplane** provisions cloud resources (databases, buckets, DNS) as Kubernetes CRs

## Relation to ApeiroRA

ApeiroRA covers similar ground with a broader scope:

- [[Platform-Mesh]] provides the overarching platform architecture (BACK Stack addresses a subset)
- [[OpenMFP]] offers an alternative/complementary micro-frontend portal approach alongside Backstage
- CNOE's [[IDP-Reference-Implementation]] is another CNCF-aligned IDP reference that overlaps with BACK Stack (both use Backstage + Argo CD)
- ApeiroRA adds layers BACK Stack does not address: [[Managed-Kubernetes-as-a-Service]] (Gardener), [[Data-Fabric]], [[AI-Agents-Overview]]

The BACK Stack is a good **starting point** for teams building an IDP with minimal components. ApeiroRA extends this into a full enterprise reference architecture.

## See Also

- [[CNCF-Platforms-White-Paper]]
- [[Platform-Maturity-Model]]
- [[CNOE]]
- [[IDP-Reference-Implementation]]
