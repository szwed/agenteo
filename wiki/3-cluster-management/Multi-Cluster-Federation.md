# Multi-Cluster Federation

Single clusters cannot span diverse regions or cloud providers due to:
- **Network latency and bandwidth** across geographies
- **Data gravity** -- cost of moving large data volumes
- **Storage replication** limits across regions
- **Control plane bottlenecks** at scale

Multi-cluster reasons: global service delivery, scalability beyond single-cluster limits, isolation/security, hybrid cloud, disaster recovery, regulatory compliance.

## Three Federation Approaches

### Centralized Federation

Central cluster extends API with federation controllers; work plane is the set of remote payload clusters. Projects: KubeAdmiral, Liqo, Karmada, KubeVela.

Challenges: complex backup/restore across distributed workloads, limited separation of concerns (runtime API discoverable), scalability bottlenecks (thundering herd), security risks (central credential store, lateral movement), network constraints (forward-connect required to all payloads).

### Agent-Based / Clusterlets

Inspired by kubelet design. Each payload cluster hosts a dedicated agent.

- **Sharded responsibility** -- management distributed across agents
- **Reversed access direction** -- agents connect outbound to central plane (inside-out), payloads stay behind firewalls
- **Enhanced separation** -- no central credential store; agent permissions scoped to its own digital twins

A **clusterlet** bundles all controllers an agent needs. Clusterlets register payload clusters (with capabilities) in the central data plane. A federation scheduler handles workload assignment.

### Separated Planes

Most advanced: central cluster reduced to a **pure data plane** (generic API server + persistence, no runtime). kcp implements this "clusterless" approach. Federation controllers run on a separate, admin-managed runtime cluster.

Benefits: superior resiliency (data plane decoupled from runtime), independent backup/restore, dynamic infrastructure (clusters as cattle, on-demand provisioning via [[Managed-Kubernetes-as-a-Service]]).

## Cluster API as a Building Block

[[Cluster-API]] provides a foundational management-cluster-to-workload-clusters pattern that underpins multi-cluster architectures. A single CAPI management cluster declaratively provisions and manages the lifecycle of many workload clusters across infrastructure providers. While CAPI itself is not a federation system, it supplies the cluster provisioning layer that federation tools (Karmada, KubeVela, etc.) build upon.

## Additional Considerations

Policy enforcement, observability, cost management, federated IAM, network overlays, GitOps/CD, disaster recovery, BCP, stateful workload management, developer experience, vendor lock-in mitigation.
