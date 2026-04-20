# Kratix

Source: [syntasso/kratix](https://github.com/syntasso/kratix)
Docs: [docs.kratix.io](https://docs.kratix.io/)

## What Is Kratix?

Kratix is an open-source **platform-as-a-product framework** by Syntasso. It enables platform teams to build internal platforms that offer self-service capabilities to application teams via declarative APIs.

The name comes from Greek: *kratiste mia yposchesi* — "keep a promise."

## Core Concepts

### Promises

A **Promise** is the contract between a platform team and its users. It defines:

- A **declarative API** (CRD) that users interact with to request a capability
- **Workflows** that execute when a user makes a request (provision, update, delete)
- **Dependencies** that must exist on destination clusters

Promises are the unit of platform capability. Examples: "PostgreSQL-as-a-Service", "Development Environment", "Monitoring Stack".

### Workflows

Workflows codify the platform team's policies, compliance requirements, and governance rules. When a user requests a resource via a Promise API:

1. The request passes through a **pipeline** of workflow steps
2. Steps can validate, transform, enrich, or reject the request
3. Steps can inject security policies, add labels, configure backups, etc.
4. The resulting resources are scheduled to destination clusters

### Multi-Cluster by Design

Kratix separates the **platform cluster** (where Promises are defined and requests are received) from **worker/destination clusters** (where resources are deployed). This maps naturally to multi-cluster architectures.

## Key Properties

- Runs on Kubernetes but can manage **non-Kubernetes resources** (cloud services, VMs, SaaS)
- Promises are **composable** — a Promise can depend on or include other Promises
- Platform teams define **what** is offered; workflows define **how** (policy, compliance, defaults)
- Users get a **self-service API** without needing to understand the underlying implementation

## Mapping to ApeiroRA

Kratix's concepts align closely with ApeiroRA patterns:

| Kratix | ApeiroRA |
|---|---|
| Promise | [[Managed-Service-Provider-Pattern]] — both define a contract for offering capabilities via declarative API |
| Promise API (CRD) | [[KRM]] / [[Digital-Twins-Extensibility]] — extending Kubernetes API with domain resources |
| Workflows | [[Security-Compliance-Automation]] + [[Validation-and-Policy]] — codified governance |
| Platform cluster | [[Service-Provider-Control-Planes]] — centralized control plane for service definitions |
| Worker clusters | [[Control-Data-Work-Planes]] — separation of control, data, and work planes |

Kratix can serve as an **implementation technology** within the [[Platform-Mesh]] for defining and delivering [[Service-Concepts]].

## See Also

- [[Service-Concepts]]
- [[Managed-Service-Provider-Pattern]]
- [[Platform-Mesh]]
- [[CNCF-Platforms-White-Paper]]
