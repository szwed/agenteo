# Validation and Policy

Validation and policy enforcement form the guardrail layer of a cloud-native platform. They ensure that resources entering or running in a cluster meet security, compliance, and organizational requirements. CNOE identifies validation as a core IDP capability; ApeiroRA embeds it in the [[Digital-Twins-Extensibility]] model through CRD validation and CEL expressions.

## API Validation

Kubernetes provides built-in validation through OpenAPI v3 schemas defined in CRDs. When a resource is submitted to the API server, it is validated against the schema before admission.

- **Structural schemas** -- Required fields, types, enums, ranges
- **CEL (Common Expression Language)** -- Kubernetes 1.25+ supports CEL validation rules directly in CRD definitions. Complex cross-field validation without external webhooks.

This is the first line of defense: malformed resources are rejected before any controller sees them. See [[Digital-Twins-Extensibility]] for how ApeiroRA uses CRD validation and CEL.

## Admission Control as Policy Plane

Beyond schema validation, Kubernetes admission controllers enforce organizational policy:

### Validating Admission Webhooks
External policy engines evaluate resources during admission and accept or reject them.

**Key tools:**
- **OPA Gatekeeper** -- Open Policy Agent integrated with Kubernetes admission. Policies written in Rego. Constraint templates define reusable policy patterns.
- **Kyverno** -- Kubernetes-native policy engine. Policies written as Kubernetes resources (YAML). Supports validate, mutate, generate, and verify-images rules.

### Mutating Admission Webhooks
Automatically modify resources to inject defaults, sidecars, labels, or annotations. Often used alongside validation to ensure compliance without requiring developers to know every requirement.

## Guardrails for Security and Regulatory Compliance

Policy engines enforce:

- **Security policies** -- No privileged containers, required security contexts, image pull policies, network policies
- **Regulatory requirements** -- Resource tagging, encryption mandates, data residency constraints
- **Organizational standards** -- Required labels (cost center, team), resource limits, naming conventions

These guardrails complement [[Infrastructure-as-Code]] -- Crossplane compositions encode infrastructure policy, while admission controllers enforce cluster-level policy.

## Binary Authorization with Signing

Validation combines with cryptographic signing ([[Signing-and-Supply-Chain]]) for binary authorization:

1. CI pipeline builds and signs container images
2. Admission controller verifies signatures before allowing deployment
3. Only images from trusted pipelines with valid attestations are admitted

Kyverno and OPA Gatekeeper both support image signature verification (e.g., with Sigstore/cosign). This connects the supply chain integrity layer to runtime enforcement.

## CNOE Perspective

CNOE includes "CNOE Validators" in its technology choices (see [[CNOE-Technology-Choices]]). The reference implementation recommends OPA Gatekeeper or Kyverno alongside Crossplane compositions that embed policy as infrastructure defaults.

The approach follows the "standardized to the infrastructure, customizable by the developers" tenet -- policy is enforced transparently, developers do not need to manage it.

## See Also

- [[Digital-Twins-Extensibility]] -- CRD validation, CEL expressions
- [[Signing-and-Supply-Chain]] -- Cryptographic integrity verification
- [[Security-Compliance-Automation]] -- Broader compliance automation
- [[Infrastructure-as-Code]] -- Policy embedded in IaC abstractions
- [[Platform-Mesh-Security]] -- Security across the platform mesh
- [[CNOE]] -- Framework overview
