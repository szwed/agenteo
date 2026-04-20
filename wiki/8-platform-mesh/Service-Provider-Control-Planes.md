# Service Provider Control Planes

Control planes translate declarative intentions into real-world implementations. They bridge service management and actual capabilities.

## How They Work

- Implement the service management component with lifecycle management API
- Based on the Kubernetes Resource Model (KRM) for consistent capability expression via digital twins
- Declarative intentions (resources) managed in service orchestration environment; controllers reconcile desired vs actual state through continuous reconciliation
- Manage entire capability lifecycle: provisioning, updates, decommissioning

## Value

- **For providers** - standardized way to expose services via declarative API while controlling implementation details
- **For consumers** - consistent interface for discovering, requesting, and managing capabilities across providers

Control planes support the [[Managed-Service-Provider-Pattern]] with APIExports reconciled by remote components on the provider's environment.

See also: [[Platform-Mesh]]
