# Infrastructure as Code (IaC)

Infrastructure as Code manages infrastructure through declarative definitions rather than manual processes. In the CNOE and ApeiroRA context, IaC builds on the infrastructure-as-a-service layer and connects to the [Controller Pattern](Controller-Pattern.md) for continuous state management.

## Two Reconciliation Models

### Occasionally Reconciled

Tools that run on demand (triggered by a pipeline or operator action) and apply changes as a point-in-time operation.

- **Terraform** -- HCL-based, plan/apply model. State file tracks resources. Runs as a batch job; drift between runs is not automatically corrected.
- **Pulumi** -- General-purpose languages (TypeScript, Python, Go) instead of DSL. Same plan/apply model as Terraform.
- **AWS CDK / CDKTF** -- Higher-level constructs that synthesize to CloudFormation or Terraform. Convenient abstractions but still occasionally reconciled.

### Continuously Reconciled

Tools that run as Kubernetes controllers, continuously watching desired state and reconciling actual state to match. This is the same [Controller Pattern](Controller-Pattern.md) used by ArgoCD for application delivery.

- **Crossplane** -- Defines infrastructure as [KRM](KRM.md) resources (CRDs). Compositions create higher-order abstractions. Providers manage AWS, GCP, Azure resources. Drift is automatically corrected because the controller loop never stops.
- **AWS Controllers for Kubernetes (ACK)** -- AWS-native controllers that expose AWS services as Kubernetes CRDs. Narrower scope than Crossplane but directly supported by AWS.

The continuously reconciled model aligns naturally with GitOps ([GitOps and Repositories](GitOps-and-Repositories.md)) -- infrastructure definitions live in Git, ArgoCD syncs them to the cluster, and Crossplane/ACK reconcile them to cloud APIs.

## Higher-Order Abstractions and Sane Defaults

Raw infrastructure resources (VPCs, subnets, S3 buckets) are too granular for most developer self-service. Both models support abstraction:

- **Crossplane Compositions** -- Combine multiple resources into a single claim. Embed organizational requirements (tagging, encryption, networking) as defaults. Developers request a "Database" without specifying every parameter.
- **Terraform Modules** -- Reusable configurations with input variables and sane defaults. Published in registries.

In the CNOE reference implementation, Crossplane compositions enforce security and governance requirements. For example, an S3 bucket composition can mandate encryption keys and tagging, continuously enforcing these even if someone changes settings manually.

## CNOE Perspective

CNOE endorses both Terraform and Crossplane (see [CNOE Technology Choices](../CNOE-Technology-Choices.md)). The choice depends on organizational context:

- Crossplane fits teams that want Kubernetes-native, continuously reconciled infrastructure with GitOps.
- Terraform fits teams with existing HCL codebases and batch-oriented workflows.
- Both can coexist. The Terraform Controller runs Terraform modules inside Kubernetes, bridging the two models.

## Relation to ApeiroRA

In the 7-layer architecture, IaC operates at the Kubernetes layer, using the Kubernetes API server as its control plane. Crossplane's KRM-based approach aligns with [KRM Bi Directional](KRM-Bi-Directional.md) -- infrastructure resources are managed through the same API patterns as application workloads.

The [IDP Reference Implementation](../10-portals/IDP-Reference-Implementation.md) demonstrates Crossplane with AWS providers, showing how developers self-service cloud resources through Backstage templates and GitOps.

## Crossplane Deep Dive

[Crossplane](Crossplane.md) (CNCF Graduated) is the primary continuously reconciled IaC tool in the ecosystem. Key v2.0 concepts:

- **Managed Resources (MRs)** -- 1:1 mapping to external cloud resources (RDS instances, S3 buckets, VPCs). Each MR is a Kubernetes custom resource continuously reconciled by a Provider controller; drift is automatically corrected.
- **Composite Resource Definitions (XRDs)** -- Define custom platform APIs (e.g. `MyDatabase`) as higher-order CRDs. Teams expose simplified interfaces hiding infrastructure complexity. See [Digital Twins Extensibility](Digital-Twins-Extensibility.md).
- **Compositions** -- Templates that map XRDs to sets of managed resources. Use a pipeline of Composition Functions to determine what resources to create.
- **Composition Functions** -- Programmable logic (Go, Python, KCL, CUE) that replaces static YAML templates. Functions run as gRPC servers; Crossplane calls them in pipeline order, passing accumulated desired state.
- **Providers** -- Packages that extend Crossplane with new managed resources. Major providers: AWS, Azure, GCP, Kubernetes, Helm. Each Provider installs its own CRDs and controller pod.
- **Operations (v2.0)** -- New alpha feature for imperative-style tasks alongside declarative resources. Three modes: `Operation` (run once), `CronOperation` (scheduled), `WatchOperation` (event-driven). Uses the same function pipeline mechanism.
- **ArgoCD Integration** -- Crossplane resources are managed via GitOps. Requires annotation-based resource tracking, custom Lua health checks, and `ProviderConfigUsage` exclusion. See [CI CD](CI-CD.md).

## See Also

- [KRM](KRM.md) -- Kubernetes Resource Model underlying Crossplane
- [Controller Pattern](Controller-Pattern.md) -- Reconciliation loop for continuously reconciled IaC
- [CI CD](CI-CD.md) -- IaC changes flow through CD pipelines
- [Control Data Work Planes](Control-Data-Work-Planes.md) -- Where IaC fits in the plane model
- [CNOE](../CNOE.md) -- Framework overview
