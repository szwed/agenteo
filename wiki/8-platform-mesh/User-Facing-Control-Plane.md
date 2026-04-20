# User-Facing Control Plane (kcp)

kcp is the foundation for Platform Mesh service management. Extracts the declarative API control plane of Kubernetes as a standalone project for orchestrating digital services (removes container orchestration).

## Hierarchical Workspaces

Workspaces provide isolated Kubernetes-like control planes with own API resources and objects. Hierarchical by nature (tree structure, fully-qualified paths). Maps directly to the [Platform Mesh Account Model](Platform-Mesh-Account-Model.md).

Workspace types define default APIs and restrict tree branches to specific aspects.

## APIExport / APIBinding

Service providers define API resource schemas via **APIExport**. Consumers **bind** to these offerings, making APIs available in their workspace. Providers get access to all objects from their APIExport via special endpoints for reconciliation. Access limited to APIs they provide, guarded by authorization checks.

Directly supports the [Managed Service Provider Pattern](Managed-Service-Provider-Pattern.md).

## Marketplace Support

APIExports and APIBindings create a marketplace experience. Consumers browse available APIs and select services. API schema provides a strong contract between provider and consumer.

## Consumer Experience

Unified KRM API surface for declarative service consumption across providers. Cross-provider compositions via standard resources (e.g. Secret exchange). Interaction via [OpenMFP](../5-software-delivery/OpenMFP.md), kubectl, IaC, or GitOps.

See also: [Platform Mesh](Platform-Mesh.md)
