# Digital Twins Extensibility

## Custom Resource Definitions (CRDs)

CRDs let users define new resource types beyond the built-in set. The extended API supports create, get, list, watch, update, patch, delete -- identical to native resources. Supports OpenAPI v3 validation, CEL validation, multi-versioning.

Defined via `apiVersion: apiextensions.k8s.io/v1`, `kind: CustomResourceDefinition`.

## Extension API Server

Alternative: extend the API server with additional APIs not part of core Kubernetes.

Example: **Gardener** is implemented as an Extension API Server. Its main user-facing resource is `Shoot` (`apiVersion: core.gardener.cloud/v1beta1`), fully adhering to [KRM](KRM.md) framework.

## Higher-Order CRDs: Crossplane XRDs

[Crossplane](Crossplane.md) introduces Composite Resource Definitions (XRDs), which are CRDs that define other CRDs. An XRD creates a new platform-specific API endpoint (e.g. `mydatabases.example.org`) backed by an OpenAPI v3 schema. When applied, Crossplane auto-generates the underlying Kubernetes CRD -- platform teams define the abstraction, and developers consume it without knowing the implementation details. This is the extensibility model in action at a higher order of abstraction.

## Discovery

`api-resources` command enables dynamic discovery of all resource definitions, their scope, API versions, and groups. Useful for RBAC policies, compatibility checks, and CLI completion.

## Usage Beyond Kubernetes

KRM serves as base representation for SDKs, clients, and tooling. The declarative approach works outside Kubernetes too.

Example: [Tilt](https://tilt.dev/) uses `tilt api-resources` with KRM-style resource definitions (`tilt.dev/v1alpha1`) in its CLI, outside the Kubernetes realm.
