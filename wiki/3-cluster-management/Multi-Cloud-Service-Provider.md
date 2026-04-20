# Multi-Cloud Service Provider

Pattern for service providers delivering services _near_ consumers across the cloud-edge continuum for technical efficiency and legal compliance.

## How It Works

1. Consumer creates a resource document via the service provider's API / data plane
2. A **scheduler controller** assigns the request to an adequate runtime environment, updating the document with the environment identifier
3. If no suitable environment exists, an autoscaler controller provisions one (delegated to a [Managed K8s Provider](Managed-Kubernetes-as-a-Service.md))
4. Each runtime hosts a **servicelet** -- watches resource documents for its identifier, implements business logic to manage the capability locally

## Key Properties

- **Reversed request direction** -- servicelet operates within/near the runtime, behind a firewall; no direct access by provider needed
- **Scales from zero** -- dynamic provisioning of runtime environments across multi-provider cloud-edge continuum
- **Status reporting** -- servicelet reports capability status back to the data plane; provider can update or dismantle runtimes accordingly

The API must adhere to [KRM](../4-kubernetes/KRM.md). The [Multi Cluster Federation](Multi-Cluster-Federation.md) pattern serves as implementation recommendation.

Pattern is not Kubernetes-exclusive -- any specialized runtime managed by a compatible runtime provider works (e.g., JVM runtimes via a Managed JVM Provider). Kubernetes can function as a generic underlying layer for any specialized runtime provider.
