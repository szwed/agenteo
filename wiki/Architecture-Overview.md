# Architecture Overview

Open-source components for the cloud-edge continuum -- uniform infrastructure from large data centers to small edge environments.

## Layers (Top to Bottom)

| Layer | Description |
|---|---|
| **Platform Mesh** | Service providers offer services; consumers discover, order, and manage lifecycle. Single integration point for non-Apeiro services. |
| **Data Fabric** | Standards and tooling for decentralized self-describing application resources. |
| **Konfidence** | Software delivery framework for microservice SaaS -- ring deployments, feature toggles, CNCF-based. |
| **Kubernetes** | Vanilla K8s for cloud-native workloads. |
| **Gardener** | Managed Kubernetes-as-a-Service across infra providers. Nodes run [[Operating-Systems|Garden Linux]]. |
| **IronCore / CobaltCore** | IaaS flavors -- compute, network, storage. CobaltCore = OpenStack API; IronCore = declarative K8s-style. |
| **Bare Metal Automation** | Manage bare metal via K8s principles, BMC/Redfish. |

## Cross-Cutting Concerns

- **Lifecycle Tooling** -- cloud-native software lifecycle at scale
- **Security & Compliance** -- built into every layer
- **Zero-Trust** -- security paradigm across Apeiro
- **Observability** -- available through all layers

## Key Principles

- **Declarative approach** across all components (like Kubernetes)
- **Kubeception** -- Kubernetes running Kubernetes (hosted control planes)
- Layers can be adopted individually; no all-or-nothing requirement

## IPCEI-CIS Mapping

| IPCEI-CIS Layer | Apeiro Components |
|---|---|
| Virtualization | Garden Linux, CobaltCore, IronCore |
| Cloud Edge Platform | Gardener |
| Service Orchestration | Platform Mesh |
| Data | Open Resource Discovery |
| Application | Konfidence |
| Management | Greenhouse, OpenMFP, OpenMCP, OCM |
