# Platform Mesh Design Decisions

## Managed Service Provider Pattern

Cloud environments require dynamic on-demand capability creation (unlike on-premises explicit installation). This necessitates **Managed Service Providers (MSPs)** -- services that manage capability lifecycles with a standardized declarative management API.

Two bundled service types:
- **Service management** - lifecycle management API (must be declarative)
- **Managed capabilities** - requested by users, orchestrated in desired contexts

Service and management runtimes may share infrastructure but separation is best practice for independent scaling.

See also: [[Managed-Service-Provider-Pattern]]

## Uniform KRM API Layer

Uniform API for ordering, managing, and orchestrating capabilities using the Kubernetes Resource Model. Leverages [[User-Facing-Control-Plane|kcp]] for logical isolation and scalability while maintaining Kubernetes API compatibility.

Every participant should provide such an API layer; consumer-facing API layers MUST provide this interface.

See also: [[Platform-Mesh]]
