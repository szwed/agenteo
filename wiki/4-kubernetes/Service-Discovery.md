# Service Discovery

Service discovery provides dynamic lookup of service APIs so that consumers can find and connect to services without hardcoded addresses. In cloud-native platforms, where services scale, move, and restart constantly, discovery is foundational.

## The Problem

In dynamic environments, service instances have ephemeral IP addresses and ports. Hardcoding endpoints breaks when instances scale, fail, or redeploy. Service discovery provides an indirection layer: services register their availability, and consumers query the registry to find them.

## Service Registries

### DNS-Based
- **Kubernetes DNS (CoreDNS)** -- Built-in service discovery for in-cluster services. Every Kubernetes Service gets a DNS entry (`my-svc.my-namespace.svc.cluster.local`). Simple, zero-config for cluster-internal use.
- **External DNS** -- Synchronizes Kubernetes Service/Ingress records to external DNS providers (Route53, CloudDNS). Bridges cluster-internal and external discovery.

### Dedicated Registries
- **Consul** (HashiCorp) -- Service mesh with built-in service registry, health checking, and KV store. Works across Kubernetes and non-Kubernetes environments.
- **etcd** -- Distributed key-value store. Kubernetes itself uses etcd for state, but it can serve as a service registry for custom use cases.
- **ZooKeeper** -- Coordination service historically used for service discovery in Hadoop/Kafka ecosystems. Being replaced by Kubernetes-native alternatives in cloud-native stacks.

## Centralized vs Distributed

| Model | Description | Example |
|-------|-------------|---------|
| **Centralized** | Single registry, all services register and query it | Consul, ZooKeeper |
| **Distributed** | Discovery embedded in the platform (DNS, service mesh) | Kubernetes DNS, Istio |

Kubernetes-native platforms favor the distributed model -- CoreDNS and service mesh sidecars handle discovery without a separate registry component.

## Integration with Config and Secret Stores

Service discovery works alongside:
- **Config repositories** ([[GitOps-and-Repositories]]) -- Service endpoints stored as config for bootstrapping
- **Secret repositories** ([[Secrets-Management]]) -- Connection credentials managed separately from discovery
- **External Secrets Operator** -- Retrieves secrets from Vault/KMS and makes them available as Kubernetes secrets, completing the bootstrapping chain: discover service, fetch credentials, connect

## CNOE and ApeiroRA Context

In CNOE's IDP model, service discovery is typically handled by Kubernetes-native mechanisms (CoreDNS, Ingress, service mesh) rather than standalone registries. The [[IDP-Reference-Implementation]] uses ingress-nginx for service routing and CoreDNS for in-cluster resolution.

In ApeiroRA, service discovery extends across the [[Platform-Mesh]] -- the [[Service-Concepts]] model and [[Managed-Service-Provider-Pattern]] define how services are published and consumed across organizational boundaries.

## See Also

- [[Service-Concepts]] -- Service model in the platform mesh
- [[Managed-Service-Provider-Pattern]] -- Cross-boundary service consumption
- [[GitOps-and-Repositories]] -- Config repos for service endpoint configuration
- [[Secrets-Management]] -- Credentials for discovered services
- [[CNOE]] -- Framework overview
