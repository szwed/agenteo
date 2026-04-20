# Cluster API (CAPI)

Kubernetes subproject (SIG Cluster Lifecycle) providing **declarative APIs for provisioning, upgrading, and operating multiple Kubernetes clusters**. An alternative to [Gardener](Managed-Kubernetes-as-a-Service.md) for cluster lifecycle management.

## Architecture

- **Management Cluster** — runs CAPI controllers, acts as single control plane for fleet of workload clusters
- **Workload Clusters** — clusters created or brought into CAPI management

All operations (provisioning, scaling, upgrades, decommissioning) are expressed as Kubernetes resource modifications.

## Core Resources

| Resource | Purpose |
|----------|---------|
| Cluster | Cluster definition (name, control plane, infrastructure provider) |
| Machine | Individual node in a workload cluster |
| MachineDeployment | Declarative desired state for a set of machines (like Deployment for Pods) |
| MachineSet | Ensures desired number of machines (like ReplicaSet) |
| MachineHealthCheck | Auto-remediation of unhealthy machines (see below) |

## MachineHealthCheck

A MachineHealthCheck defines conditions under which Machines are considered unhealthy and should be remediated (deleted and replaced). Applies only to Machines owned by a MachineSet or KubeadmControlPlane. Key features:

- **Node conditions** — monitors Node `Ready` status; if `Unknown` or `False` beyond a timeout (e.g. 300s), the Machine is remediated
- **Node startup timeout** — if no Node joins within a configurable period (default 10m), the Machine is remediated
- **Short-circuiting** — `unhealthyLessThanOrEqualTo` prevents mass remediation when too many Machines are unhealthy (e.g. set to `40%`)
- **Skip remediation** — annotations `cluster.x-k8s.io/skip-remediation` or `cluster.x-k8s.io/paused` suppress remediation (useful during `clusterctl move`)
- **KCP remediation strategy** — `maxRetry`, `retryPeriod`, and `minHealthyPeriod` control remediation retries for control plane nodes

## Autoscaling

CAPI integrates with the Kubernetes [Cluster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler) via its CAPI cloud provider. Autoscaler adjusts MachineDeployment/MachineSet replicas based on pod scheduling demand. Min/max size is configured via annotations on MachineDeployment/MachineSet; the replicas field is auto-defaulted to stay within the annotated range.

## Provider Types

1. **Infrastructure providers** — provision VMs, load balancers, VPCs (AWS, Azure, GCP, OpenStack, vSphere, metal3.io, MAAS)
2. **Control plane providers** — handle control plane lifecycle (kubeadm, Talos, k3s, MicroK8s)
3. **Bootstrap providers** — deliver Kubernetes onto nodes (kubeadm, Talos, EKS)

## Pivoting

CAPI supports the pivoting process via `clusterctl move` -- transferring CAPI objects (Cluster, Machine, MachineDeployment, etc.) from a source management cluster to a target. Typical bootstrap-and-pivot flow:

1. Create a temporary bootstrap cluster (e.g. kind)
2. `clusterctl init` to install providers; create the target management cluster
3. `clusterctl init` on the target cluster to install providers there
4. `clusterctl move --to-kubeconfig=<target>` to migrate all CAPI resources
5. Delete the bootstrap cluster

Before moving, `clusterctl` sets `Cluster.Spec.Paused=true` to stop reconciliation on the source. Use `--namespace` to target a specific namespace and `--dry-run` to preview without changes. Status subresources are never restored -- controllers rebuild them from spec. See [Data and Control Plane State](../4-kubernetes/Data-and-Control-Plane-State.md) for the general concept.

## CAPI vs Gardener

| Aspect | Cluster API | Gardener |
|--------|-------------|----------|
| Approach | Building blocks — assemble your own | Opinionated, batteries-included |
| Control Plane | Varies by provider | [Hosted Control Planes](Hosted-Control-Planes.md) (Kubeception) |
| Multi-cloud | Via multiple infra providers | Built-in extension mechanism |
| Fleet management | Manual or via GitOps | Centralized (Garden → Seed → Shoot) |
| Auto-scaling | External (e.g., cluster-autoscaler) | Built-in (control plane + workers) |
| Live migration | Not built-in | Built-in control plane migration |
| Best for | Custom platforms, bottom-up assembly | Enterprise managed K8s-as-a-Service |

Both use [KRM](../4-kubernetes/KRM.md) and the [Controller Pattern](../4-kubernetes/Controller-Pattern.md) for declarative cluster management.

## Security Guidelines

Based on the [CAPI Security Self-Assessment](https://github.com/kubernetes/sig-security/blob/main/sig-security-assessments/cluster-api/self-assessment.md):

- **Least privilege** -- dedicated cloud credentials with minimal permissions; separate creds for management vs workload clusters
- **Cluster isolation** -- separate workload and management clusters at network (VPC) and account/subscription level; independent CAs per cluster
- **Audit and alerting** -- enable API server audit logging on both management and workload clusters; monitor for unauthorized resource changes
- **Immutable infrastructure** -- disable SSH and runtime modifications to nodes; changes require new machine images
- **Second pair of eyes** -- enforce review workflows (e.g. GitOps PRs) for privileged cluster operations

## Links

- [Cluster API Book](https://cluster-api.sigs.k8s.io/)
- [GitHub](https://github.com/kubernetes-sigs/cluster-api)
- [Provider List](https://cluster-api.sigs.k8s.io/reference/providers)

See also: [Managed Kubernetes as a Service](Managed-Kubernetes-as-a-Service.md), [Multi Cluster Federation](Multi-Cluster-Federation.md), [Hosted Control Planes](Hosted-Control-Planes.md), [Data and Control Plane State](../4-kubernetes/Data-and-Control-Plane-State.md)
