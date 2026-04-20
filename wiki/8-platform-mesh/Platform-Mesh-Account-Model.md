# Platform Mesh Account Model

Powered by kcp. Hierarchical account structure where each account functions as an isolated control plane.

## Account Structure

Hierarchical model mirroring organizational structure (Organization -> Teams -> Staging/Production/Dev). Deep nesting, logical isolation, built-in account types, policy flow through hierarchy.

## Service Management Integration

Automated relationship management between consumers and providers. Creates shadow accounts and tenant spaces automatically. Leverages KRM for declarative service consumption and the [[Managed-Service-Provider-Pattern]]. Marketplace-like experience for service discovery.

## Identity Management

Consistent authentication across the platform. Integrates with existing identity providers while maintaining organizational control.

## Key Management

Leverages [[Key-Management|OpenKCM]] for account-level data protection. HSM-protected root keys (L1), keychain hierarchy (L2-L4 via Krypton), key rotation policies, granular access controls.

## Service Orchestration

Choreography-based (not central orchestrator). Services manage functions autonomously; desired behavior emerges from collaboration. Dedicated orchestration contexts group related services. Supports both managed and unmanaged services.

See also: [[User-Facing-Control-Plane]], [[Platform-Mesh]]
