# Platform Mesh Guiding Principles

## Declarative API

Solely declarative model, no imperative requests. Inherited from the Kubernetes Resource Model (KRM) -- generic API server with extensible resource types.

REST manages declaration resources only. Controllers/operators handle real-world drift control on top of the REST model. The service orchestration environment provides a structured object space for desired state; controllers reconcile desired vs actual state.

## Decoupling

All components usable without the complete framework. Service providers should be self-contained with their own tenant/account management (linkable to corporate systems or orchestration environment).

The architecture avoids bundling functionality that could be separate, maximizing flexibility in composition. Marketplaces are a central element but should not be required for other parts to function.

See also: [Platform Mesh](Platform-Mesh.md)
