# Managed Kubernetes-as-a-Service

**Gardener** is the default (not exclusive) K8s-as-a-Service provider in the Apeiro Reference Architecture. Fully certified Kubernetes, DISA STIG checked.

## Botanical Architecture

Kubernetes-in-Kubernetes ([[Hosted-Control-Planes|Kubeception]]):

- **Garden Cluster** -- central management layer (nodeless). Brain of the Gardener landscape: API server, etcd, controllers. Users create/modify/delete shoot clusters here.
- **Seed Clusters** -- host the control planes of shoot clusters. Provide infrastructure for efficient resource utilization and operational independence.
- **Shoot Clusters** -- user-facing K8s clusters. Worker nodes are VMs in hyperscaler or own datacenter running OS + container runtime + kubelet.

## Benefits

- **Resource efficiency** -- dynamic scaling algorithms for individual control plane components, lower TCO
- **Homogeneous multi-cloud** -- extension mechanism + multi-region seeds = consistent K8s experience across providers
- **High availability** -- control plane components managed as K8s resources with liveness/readiness probes, auto-restart, live control plane migration
- **Simplified fleet management** -- manage multiple shoots from single garden cluster (updates, scaling, monitoring)

## Blueprint for MSP Pattern

Gardener architecture provided the blueprint for the [[Multi-Cloud-Service-Provider]] pattern -- a service provisioning system that initializes and manages its own hosting infrastructure across the cloud-edge continuum.

## Links

- [Gardener Getting Started](https://gardener.cloud/docs/getting-started/introduction/)
- [Gardener Website](https://gardener.cloud/)
- [Gardener GitHub](https://github.com/gardener)
