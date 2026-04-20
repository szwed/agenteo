# OpenMFP Portal

The Open Micro Frontend Platform (OpenMFP) is a platform from ApeiroRA / NeoNephos Foundation (Linux Foundation) for building portals and complex web applications through runtime micro frontend composition. It provides an opinionated, batteries-included approach to integrating UI capabilities from different teams and organizations.

## Core Concepts

### Micro Frontend Architecture

OpenMFP is built around micro frontends -- small, self-contained applications that can be developed, tested, and deployed independently. Extensions are the building blocks; nearly every feature in OpenMFP is an extension.

Three types of extensions:
1. **UI-only Micro Frontends** -- self-sufficient frontend applications running within the portal, using the [Luigi framework](https://luigi-project.io/) for composition
2. **Micro Frontends with Backend Dependencies** -- frontend combined with backend services (e.g., events)
3. **Service-only Extensions** -- backend services without a UI component

OpenMFP does not enforce how extensions are built or deployed. Owning teams maintain full autonomy over their technology choices and release cycles.

### Portal Architecture

Two main libraries:
- **portal-server-lib** -- server-side library handling configuration retrieval, context resolution, and template processing
- **portal-ui-lib** -- client-side library that dynamically evaluates installed extensions and renders the composed UI

The portal uses the Luigi framework for micro frontend integration. Micro frontends run in iframes and communicate via Luigi Client for navigation and context sharing.

### ContentConfiguration CRD

Kubernetes-native declarative API for managing micro frontend lifecycle:

```yaml
apiVersion: core.openmfp.io/v1alpha1
kind: ContentConfiguration
metadata:
  name: example-extension
  labels:
    extensions.openmfp.io: myextension
spec:
  remoteConfiguration:
    url: https://example.com/config.yaml
  # or inlineConfiguration for embedded config
```

ContentConfiguration describes how an extension integrates into the portal -- what UIs and components are displayed, where, and under what conditions. The Extension Manager Operator processes these resources asynchronously, validates them, and stores the observed state. The portal queries processed configurations at render time.

Key design properties:
- Asynchronous processing -- configuration is pre-processed before web requests
- Validation -- invalid configurations are rejected before being applied
- Supports both inline and remote configuration definitions
- 1:N relationship between ExtensionClass and ContentConfiguration resources

### Extension Manager Operator

A Kubernetes operator that manages ContentConfiguration resources. It reconciles extension configurations, downloads remote configurations, validates content, and updates status conditions. This makes UI extension lifecycle management fully Kubernetes-native.

### Account Management

Central account entity for grouping resources across integrated services, similar to a hyperscaler account. Accounts are loosely coupled with services -- each service implements its own onboarding experience while linking back to the central account. Authorization is managed via a planned ReBAC (Relationship Based Access Control) service based on OpenFGA.

### GraphQL Gateway

The kubernetes-graphql-gateway provides a GraphQL API for accessing Kubernetes resources, enabling frontend micro frontends to query cluster state through a unified API layer.

## Key Characteristics

- **Technology agnostic** -- teams choose their own frontend framework
- **Runtime integration** -- micro frontends composed at runtime, not build time
- **Kubernetes-native** -- extension lifecycle managed via CRDs and operators
- **Independent releases** -- teams release and lifecycle their extensions independently
- **Luigi-based** -- uses Luigi framework for micro frontend orchestration

## Planned Features

- **Control Plane** -- central management API leveraging kcp (Kubernetes-like Control Plane) for user-specific control plane capabilities
- **Authorization** -- central ReBAC service based on OpenFGA for unified permission management

## Relation to ApeiroRA

OpenMFP is part of the broader ApeiroRA ecosystem:
- [[Micro-Frontends]] -- micro frontend architecture in ApeiroRA software delivery
- [[OpenMFP]] -- OpenMFP in the software delivery layer
- [[Platform-Mesh]] -- developer portal sits in the platform mesh layer

Some components are being migrated to [Platform Mesh](https://platform-mesh.io/). OpenMFP continues to focus on being a micro frontend platform for UI capability and integration.

## Comparison with Backstage

| Aspect | OpenMFP | Backstage |
|---|---|---|
| Approach | Micro frontend composition runtime | Developer portal framework |
| Extension model | Independent micro frontends (any framework) | Plugins within a single React app |
| K8s integration | Native (CRDs, operators) | Views K8s resources via plugin |
| Catalog | Not primary focus | Core feature |
| Governance | NeoNephos Foundation (Linux Foundation) | CNCF Graduated |

See [[Backstage]] for full Backstage documentation.

## Links

- https://openmfp.org
- https://github.com/openmfp
- [[Portals-Overview]] -- comparison of portal approaches
- [[Developer-Portal]] -- developer portal as an IDP capability
