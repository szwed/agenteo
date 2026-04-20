# Services

A **service** is an entity offering some API to consumers. APIs can be REST, event/pub-sub, binary protocols, or service-specific protocols. Multiple providers may offer identical APIs (e.g. same open-source database).

## Capability

Specific configured instance of a service. Two categories:
1. **Deployment-based** - requires software deployment and infrastructure allocation (e.g. database setup)
2. **Tenant-based** - maps to a tenant in existing SaaS; no new deployment needed (e.g. DB schema, billing entry)

A capability + its resource = digital twin.

## Resource

KRM description of desired state of a capability. Consumer creates/modifies/deletes; provider's controller detects and reconciles.

## Service Provider

Entity that offers services, monitors resources, manages capabilities. Operates a controller watching for resource changes. Responsible for digital twin synchronization. Recommended: [Managed Service Provider Pattern](Managed-Service-Provider-Pattern.md).

## Managed vs Unmanaged

- **Managed** - delivered through a service provider with declarative lifecycle management
- **Unmanaged** - set up by DevOps outside Apeiro; only for legacy systems

## Marketplace

Allows providers to register services for consumers to discover. Connects to service orchestration environments.

## Service Runtime

| Service | Runtime |
|---|---|
| VM | Hypervisor |
| K8s Cluster | VM |
| Database | K8s Cluster |
| DB Schema | Database |
| SaaS | PaaS, Database |

See also: [Platform Mesh](Platform-Mesh.md)
