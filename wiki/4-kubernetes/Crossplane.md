# Crossplane

Crossplane is a CNCF Graduated project that turns any Kubernetes cluster into a cloud infrastructure control plane. It lets platform teams build custom APIs (using the [[KRM]] pattern) without writing controllers, and continuously reconciles desired state to actual state across cloud providers.

## Core Concepts

- **Managed Resources (MRs)** -- Kubernetes custom resources that represent external cloud resources 1:1 (e.g. an RDS instance, an S3 bucket). A Provider controller watches each MR and creates/updates/deletes the corresponding external resource. `forProvider` is the source of truth; manual drift is automatically corrected.
- **Composite Resource Definitions (XRDs)** -- Higher-order CRDs that define platform-specific APIs (see [[Digital-Twins-Extensibility]]). An XRD creates a new API endpoint (e.g. `mydatabases.example.org`) with an OpenAPI v3 schema. Developers consume the simplified API without knowing the underlying resources.
- **Compositions** -- Templates that map an XR (composite resource) to a set of managed or Kubernetes resources. Each Composition defines a pipeline of Composition Functions.
- **Composition Functions** -- gRPC-based plugins that implement composition logic in real programming languages (Go, Python, KCL, CUE, or YAML templates). Functions receive observed state and return desired state. They run in a pipeline, each building on the previous function's output.
- **Providers** -- Packages that extend Crossplane with new managed resources and their controllers. Major providers: AWS (`provider-upjet-aws`), Azure (`provider-upjet-azure`), GCP (`provider-upjet-gcp`), Kubernetes (`provider-kubernetes`), Helm. Installed via the Crossplane package manager.

## v2.0 Highlights

- **Operations** (alpha) -- Imperative-style tasks alongside declarative resources. Three modes:
  - `Operation` -- run a function pipeline once to completion (like a Job)
  - `CronOperation` -- run on a schedule
  - `WatchOperation` -- run when watched resources change
  - Use case: certificate monitoring, rolling upgrades, scheduled maintenance
- **Namespaced by default** -- XRDs default to `Namespaced` scope for better security isolation
- **Required resources** -- Functions can request existing cluster resources (ConfigMaps, etc.) via bootstrap requirements in the Composition or dynamic requests at runtime
- **Function response caching** -- Alpha feature to cache function responses for improved performance

## Relation to ApeiroRA

Crossplane is the canonical example of the **Actuator** archetype (see [[Controller-Archetypes]]): Provider controllers map real-world cloud capabilities into the Kubernetes virtual world as digital twins. It extends [[KRM]] beyond the cluster boundary to cloud resources, making infrastructure management indistinguishable from application management at the API level.

In the [[Infrastructure-as-Code]] taxonomy, Crossplane is the primary **continuously reconciled** IaC tool -- drift is corrected automatically by the controller loop, unlike occasionally reconciled tools (Terraform, Pulumi) that only detect drift on the next run.

## GitOps Integration

Crossplane integrates with ArgoCD (see [[CI-CD]]) for GitOps-driven infrastructure. Configuration requirements:
- Annotation-based resource tracking (`application.resourceTrackingMethod: annotation`)
- Custom Lua health checks for Crossplane resource types
- Exclusion of `ProviderConfigUsage` resources from ArgoCD UI
- Increased Kubernetes client QPS (`ARGOCD_K8S_CLIENT_QPS: 300`) for clusters with many CRDs

## Links

- [crossplane.io](https://crossplane.io)
- [GitHub: crossplane/crossplane](https://github.com/crossplane/crossplane)
- [Crossplane Docs v2.0](https://docs.crossplane.io)

## See Also

- [[Infrastructure-as-Code]] -- Crossplane as continuously reconciled IaC
- [[KRM]] -- Kubernetes Resource Model that Crossplane extends to cloud resources
- [[Controller-Archetypes]] -- Crossplane Providers as actuator archetype
- [[Digital-Twins-Extensibility]] -- XRDs as higher-order CRDs
- [[CI-CD]] -- ArgoCD integration for GitOps
- [[Controller-Pattern]] -- Reconciliation loop underpinning Crossplane
