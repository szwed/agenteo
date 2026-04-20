# Kubernetes Resource Model

Kubernetes uses an opinionated [Digital Twin](Digital-Twins.md) model. KRM defines a declarative approach: describe "desired state" of resources, software actuators (controllers/operators) reconcile with actual state.

## Key Design Principles

- Founded on **Promise Theory** (not imperative command & control)
- Cloud-native reference for immutable infrastructure: predictability, repeatability, scalability, reversibility, availability
- **API centric but not API driven** -- all requests go via API server, but all business logic runs outside it in decoupled controllers. This is why the API is uniformly extendable.
- Extended beyond in-cluster via CRDs to represent real-world resources

## Resource Structure

- **group, version, kind** -- uniquely identifies the resource type
- **metadata** -- names, namespace, labels, annotations
- **spec** -- desired state
- **status** -- actual state feedback

## Design Choices and Limitations

- No uniform status property -- requires individual/domain-specific interpretation
- Eventual consistency challenges inherent to distributed systems
- Optimistic concurrency control using shared repository state

See also: [KRM Bi Directional](KRM-Bi-Directional.md), [KRM Control](KRM-Control.md), [KRM Format](KRM-Format.md), [KRM Kubernetes](KRM-Kubernetes.md)
