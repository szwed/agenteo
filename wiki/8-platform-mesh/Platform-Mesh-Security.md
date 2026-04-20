# Platform Mesh Security

## Authentication

Standardized on **OIDC**. kcp also supports Kubernetes service accounts natively.

- **Keycloak** as internal IDP: JWT tokens (OIDC), Authorization Code flow for portal, Auth Code + PKCE for kubectl, tenant-aligned realms per organization
- **Identity Federation**: Keycloak brokers external IDPs (corporate OIDC, SAML, LDAP) into consistent internal representation ("bring your own IDP")
- **Machine identity**: workspace-level OIDC config for Kubernetes JWT issuers, GitHub Actions OIDC, etc.

## Authorization (Two-Tier)

### Tier 1: Kubernetes RBAC

Built-in role-based access control at API resource level. Scoped per workspace (isolated control plane). Declaratively managed. Extends naturally to custom resources from service providers.

### Tier 2: OpenFGA (ReBAC)

Relationship-Based Access Control (Zanzibar approach). Access derived from relationship graph (user, relation, object) -- e.g. team membership grants service access. Integrated via kcp authorization webhook (pluggable).

### Evaluation Flow

1. RBAC evaluates first (grant/deny at resource-type level)
2. If RBAC has no opinion -> forwarded to OpenFGA for relationship-based evaluation

## Account Model Integration

- Per-organization Keycloak realm and OpenFGA store
- Dynamic authorization schema generated from bound APIs
- Hierarchical permission inheritance through relationship graph
- Service relationship authorization via export/bind mechanisms

See also: [[Platform-Mesh]], [[Platform-Mesh-Account-Model]]
