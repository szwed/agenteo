# KRM Wire and At-Rest Format

Kubernetes uses [KRM](KRM.md) format identically in transit and at rest (disk, version control, storage). The resource body contains sufficient information to construct API calls -- no additional envelope needed.

A GET returns the same body that can be stored, versioned, audited, used as backup, or promoted across environments (dev -> test -> staging -> production) for immutable infrastructure.

## Client Pattern

All KRM-compatible clients (spearheaded by `kubectl`) share a common pattern:
1. Read at-rest manifest
2. Parse `apiVersion`, `kind`, `namespace`, `name` from body
3. Construct API URL and POST to API server
4. Endpoint and credentials from applicable `kubeconfig` context
