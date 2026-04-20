# Multi-Plane Controller

Controllers can be multi-control-plane aware -- executed anywhere suitable and connected to multiple planes. Enables isolation boundaries for cloud services and [Multi Cluster Federation](../3-cluster-management/Multi-Cluster-Federation.md) design.

## Architecture Components

1. **Runtime Cluster** -- where the controller runs (as Pod). May access its own control plane for self-management, or rely on VPA/HPA.
2. **Digital Twin API Layer** -- separate data plane for user-facing API and source of truth. Intentionally separated from Runtime Cluster for isolation.
3. **Multiple Targets** -- separate clusters/control planes as scale-out targets. Isolates controller runtime from workload concerns.

## Fan-In (multicluster-runtime)

Single controller reconciles objects from multiple planes simultaneously. Standard controller-runtime does not support this. **multicluster-runtime** library extends it for dynamic fleet orchestration. Providers: kcp multicluster-provider, Gardener multicluster-provider.

## Fan-Out (cluster package)

Controller interacts with multiple clusters for create/update operations (distributing configs, secrets, workloads). `sigs.k8s.io/controller-runtime/pkg/cluster` provides distinct clients/caches per target. Combined with MultiClusterManager for efficient connection management.

## Best Practices

- **Scalability** -- leverage multicluster-runtime for dynamic multi-plane handling
- **Isolation** -- clear separation between data plane, Runtime Cluster, and targets
- **Dynamic discovery** -- MultiClusterManager for automatic cluster detection
- **Consistency** -- level-based reconciliation, well-designed [KRM](KRM.md) extensions, proper conditions/states
- **Error handling** -- exponential backoff with random delays to avoid thundering herd
