# Hosted Control Planes

**Kubeception**: recursively deploying Kubernetes with/in Kubernetes. Control and data plane components are hosted as tenant workloads in the work plane of a host/seed cluster. HCP is fundamentally a Control-Plane-as-a-Service offering.

## Benefits

- **Cost efficiency** -- control plane components run in containers (multi-tenant) instead of dedicated VMs
- **Faster provisioning** -- control/data plane treated like any cloud-native deployment
- **Security optimizations** -- planes managed separately with strong isolation between control and work plane
- **Cloud-native benefits** -- Kubernetes deploys, scales, and manages itself; all cloud-native advantages inherited

Learned Kubernetes skills become portable across all layers of the cloud stack.

## Foundation for Managed K8s-as-a-Service

HCP architecture is the basis for building [[Managed-Kubernetes-as-a-Service]] offerings -- the indispensable platform runtime service. Enables universal on-demand runtimes with portability across infrastructure providers.

Enterprise-grade K8s-as-a-Service requires more than simple HCP: dynamic seed cluster creation across heterogeneous providers/regions, autonomous operations (auto-scaling, auto-updating, self-healing), and dedicated management logic captured in a product like [[Managed-Kubernetes-as-a-Service|Gardener]].

## CAPI and Hosted Control Planes

[[Cluster-API]] supports HCP through dedicated control plane providers such as [Kamaji](https://github.com/clastix/cluster-api-control-plane-provider-kamaji), [k0smotron](https://github.com/k0sproject/k0smotron), and the [Hosted Control Plane provider](https://github.com/teutonet/cluster-api-provider-hosted-control-plane). These providers run workload cluster control planes as pods inside a management cluster rather than on dedicated VMs, bringing the cost and operational benefits of Kubeception to the CAPI ecosystem.
