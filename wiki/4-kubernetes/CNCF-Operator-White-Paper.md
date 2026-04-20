# CNCF Operator White Paper

Source: [CNCF TAG App Delivery — Operator White Paper v1.0](https://github.com/cncf/tag-app-delivery/blob/main/operator-wg/whitepaper/Operator-WhitePaper_v1-0.md)

## What Is an Operator?

An operator encapsulates domain-specific operational knowledge into software that extends a container orchestrator's API. In Kubernetes, operators combine **custom resources** (CRDs) with **custom controllers** to automate the full lifecycle of an application.

> "An operator is a Kubernetes controller that understands 2 domains: Kubernetes and something else. By combining knowledge of both domains, it can automate tasks that usually require a human operator that understands both domains." — Jimmy Zelinskie

## Operator vs Controller

There is no technical difference. The distinction is conceptual:

- A **controller** is the implementation mechanism (reconciliation loop watching resources)
- An **operator** is the pattern of using controllers with CRDs to encode **operational knowledge** (upgrades, backups, failover, remediation)

A controller that only creates a pod on CR creation is a simple controller. A controller that knows how to upgrade, backup, and auto-remediate is an operator.

See [[Controller-Pattern]] and [[Controller-Archetypes]] for ApeiroRA's treatment of the controller concept.

## Operator Design Pattern

Three components:

1. **The managed application/infrastructure** — what we want to operate
2. **A domain-specific declarative API** (CRDs) — users describe desired state
3. **A controller** — continuously reconciles actual state toward desired state, reports status

## Operator Capabilities

| Capability | Description |
|---|---|
| **Install / take ownership** | Provision all resources; adopt pre-existing resources without downtime |
| **Upgrade** | Version-aware upgrades with dependency handling, rollback on failure |
| **Backup** | Consistent snapshots to external storage (S3, NFS) |
| **Recovery** | Restore application state (version + data) from backup |
| **Auto-remediation** | Detect failures beyond liveness probes; restart, rollback, or escalate |
| **Observability** | Expose operator metrics (remediation count, backup duration, errors) |
| **Scaling** | Horizontal and vertical scaling without downtime |
| **Auto-scaling** | Metrics-driven automatic scaling with min/max bounds |
| **Auto-configuration** | Adapt config to environment (memory, DNS); handle config-change restarts |
| **Uninstall / disconnect** | Clean removal of all resources, or stop managing without deletion |

## Operator Characteristics

Three categories of value:

- **Dynamic configuration** — progressive defaults, adaptive tuning, structured validation via CRDs
- **Operational automation** — repeatable, testable lifecycle tasks (deploy, backup, scale)
- **Domain knowledge** — encoded runbooks, version-aware upgrade paths, error remediation

## Successful Patterns

- **One operator per application** — separation of concerns
- **One CRD per controller** — readability and maintainability
- **Operator of operators** — meta-operator coordinates a stack, delegates to sub-operators via internal CRDs
- **Don't install other operators** — use a package manager (OLM) for dependency resolution

## Frameworks

| Framework | Language | Notes |
|---|---|---|
| Operator SDK | Go, Helm, Ansible | Most popular; scaffolding via kubebuilder |
| kubebuilder | Go | controller-runtime based; generates CRDs, RBAC, Deployment |
| Kopf | Python | Lightweight; good for ad hoc operators |
| Metacontroller | Any (webhook) | Lambda controller pattern; no boilerplate |

## Security Best Practices

**For operator developers:**
- Document RBAC scopes, threat model, communication ports
- Publish security disclosure process
- Minimize required permissions (least privilege)

**For operator users:**
- Review installation manifests before applying
- Scope operators to namespaces when possible
- Verify software provenance (supply chain)
- Apply Pod Security Standards and network policies

## Mapping to ApeiroRA

ApeiroRA relies extensively on the operator pattern:

- [[Controller-Pattern]] covers the reconciliation loop fundamentals
- [[Controller-Archetypes]] defines ApeiroRA's taxonomy of controller types (similar to operator capability levels)
- [[Lifecycle-Management]] and [[LCM-Operator-Installation]] use operators for software delivery
- [[Digital-Twins-Extensibility]] describes extending Kubernetes via CRDs — the foundation operators build on
- [[Multi-Plane-Controller]] extends the pattern across control/data/work planes
