# Deployment Plan: 10-Layer Cloud-Native Platform

This plan covers the full deployment of a cloud-native platform from bare metal to AI agents, based on the [wiki documentation](wiki/Home.md).

Each layer builds on the previous one. Deploy in order — skip layers you don't need (e.g., start at Layer 3 if you have existing infrastructure).

---

## Layer 1 — Bare Metal Automation

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **IronCore Baremetal** | Automation | Kubernetes-native server discovery, provisioning, day-2 ops via BMC/Redfish | [wiki](wiki/1-bare-metal/Baremetal.md) |
| **Garden Linux** | OS | Minimal, secure, Debian-based Linux for K8s nodes and VMs | [wiki](wiki/1-bare-metal/Operating-Systems.md) |
| **Redfish API** | Protocol | Standardized BMC interface for server lifecycle management | — |

**Prerequisites:** Physical servers with BMC, network switches, storage.
**Outcome:** Automated server inventory and provisioning via declarative APIs.

---

## Layer 2 — Infrastructure Services

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **IronCore IaaS** | IaaS | Declarative Kubernetes-style compute, network, storage | [wiki](wiki/2-infrastructure-services/Showroom-Scenarios.md) |
| **CobaltCore** | IaaS | OpenStack-compatible compute, network, storage (alternative to IronCore) | [wiki](wiki/2-infrastructure-services/Showroom-Scenarios.md) |

**Prerequisites:** Layer 1 (bare metal automation) or existing hypervisor/cloud.
**Outcome:** IaaS APIs for provisioning VMs, networks, and storage.

---

## Layer 3 — Cluster Management

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Gardener** | Managed K8s | Garden/Seed/Shoot architecture for multi-cloud K8s-as-a-Service | [wiki](wiki/3-cluster-management/Managed-Kubernetes-as-a-Service.md) |
| **Cluster API (CAPI)** | Cluster lifecycle | Declarative cluster provisioning, upgrading, scaling (alternative to Gardener) | [wiki](wiki/3-cluster-management/Cluster-API.md) |
| **clusterctl** | CLI | CAPI management tool — init, move (pivoting), upgrade | [wiki](wiki/3-cluster-management/Cluster-API.md) |
| **gardenadm** | CLI | Gardener bootstrap and autonomous cluster management | [wiki](wiki/3-cluster-management/Managed-Kubernetes-as-a-Service.md) |

**Prerequisites:** Layer 2 (IaaS) or existing cloud provider (AWS, Azure, GCP, OpenStack, vSphere).
**Outcome:** On-demand Kubernetes clusters with automated lifecycle management.

---

## Layer 4 — Kubernetes Platform

### 4a. Core Platform

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Kubernetes** | Runtime | Container orchestration, KRM API server, etcd | [wiki](wiki/4-kubernetes/KRM.md) |
| **containerd / CRI-O** | Container runtime | OCI-compliant container runtime | — |
| **CoreDNS** | DNS | Cluster DNS resolution | — |
| **etcd** | Data store | Distributed key-value store for cluster state | [wiki](wiki/4-kubernetes/Kubernetes-Implementation-Design.md) |

### 4b. Infrastructure as Code

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Crossplane** | IaC (CNCF Graduated) | Kubernetes-native cloud resource management — XRDs, Compositions, Providers | [wiki](wiki/4-kubernetes/Crossplane.md) |
| **Crossplane AWS/Azure/GCP Providers** | Providers | Cloud-specific managed resources for Crossplane | [wiki](wiki/4-kubernetes/Infrastructure-as-Code.md) |
| **Terraform** | IaC | Occasionally-reconciled IaC (alternative/complement to Crossplane) | [wiki](wiki/4-kubernetes/Infrastructure-as-Code.md) |

### 4c. GitOps & CI/CD

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Argo CD** | CD (GitOps) | Declarative GitOps continuous delivery — reconciles Git state to cluster | [wiki](wiki/4-kubernetes/CI-CD.md) |
| **Flux CD** | CD (GitOps) | Alternative GitOps toolkit (composable source/kustomize/helm controllers) | [wiki](wiki/4-kubernetes/CI-CD.md) |
| **Argo Workflows** | CI | Kubernetes-native DAG/step workflow engine | [wiki](wiki/4-kubernetes/CI-CD.md) |
| **Tekton** | CI | Kubernetes-native CI pipeline framework (Tasks + Pipelines as CRDs) | [wiki](wiki/4-kubernetes/CI-CD.md) |
| **Gitea** | Git server | In-cluster Git server with OCI registry (used by IDPBuilder) | [wiki](wiki/10-portals/IDPBuilder-Details.md) |

### 4d. Policy & Validation

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Kyverno** | Policy engine | Kubernetes-native policy management (validate, mutate, generate) | [wiki](wiki/4-kubernetes/Validation-and-Policy.md) |
| **OPA / Gatekeeper** | Policy engine | Open Policy Agent with K8s admission controller | [wiki](wiki/4-kubernetes/Validation-and-Policy.md) |
| **Sigstore / Cosign** | Signing | Keyless artifact signing and verification (SSSC) | [wiki](wiki/4-kubernetes/Signing-and-Supply-Chain.md) |

### 4e. Workloads

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **KubeVirt** | Virtualization | Run VMs on Kubernetes (virt-api, virt-controller, virt-handler) | [wiki](wiki/4-kubernetes/KubeVirt.md) |
| **Score** | Workload spec (CNCF Sandbox) | Platform-agnostic workload definition — write once, deploy anywhere | [wiki](wiki/4-kubernetes/Score-Workload-Spec.md) |

---

## Layer 5 — Software Delivery

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Konfidence** | Delivery framework | Immutable application vectors, stage-based promotion (DEV→TEST→PROD) | [wiki](wiki/5-software-delivery/Konfidence.md) |
| **Open Component Model (OCM)** | SBoD / packaging | Software Bill of Delivery — signed, traceable, air-gap-safe delivery | [wiki](wiki/5-software-delivery/Software-Bill-of-Delivery.md) |
| **OCM Gear** | Compliance tooling | Security compliance automation with OCM coordinates | [wiki](wiki/8-platform-mesh/Security-Compliance-Automation.md) |

**Prerequisites:** Layer 4 (Kubernetes + CI/CD).
**Outcome:** Reproducible, auditable software delivery pipeline with immutable vectors.

---

## Layer 6 — Data Fabric

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Open Resource Discovery (ORD)** | Protocol | Standardized service/API metadata description | [wiki](wiki/6-data-fabric/Data-Fabric-Components.md) |
| **Unified Metadata Service (UMS)** | Aggregator | Central metadata collection, discovery API, metadata graph | [wiki](wiki/6-data-fabric/Data-Fabric-Components.md) |
| **Landscape Resource Viewer** | UI | Visual metadata graph of services and business objects | [wiki](wiki/6-data-fabric/Data-Fabric-Landscape.md) |

**Prerequisites:** Services exposing ORD endpoints.
**Outcome:** Automated service discovery, integration mapping, and metadata visualization.

---

## Layer 7 — Managed Services (Operators)

### 7a. Observability Stack

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Prometheus Operator** | Monitoring | Prometheus + Alertmanager + Grafana on K8s (ServiceMonitor, PrometheusRule) | [wiki](wiki/7-services/Prometheus-Operator.md) |
| **Elasticsearch / ECK** | Log analytics | Elasticsearch + Kibana + APM on K8s | [wiki](wiki/7-services/Elasticsearch-Operator.md) |
| **OpenTelemetry** | Telemetry | Unified logs, metrics, traces collection (OTel Collector) | [wiki](wiki/8-platform-mesh/Observability.md) |
| **Jaeger** | Tracing | Distributed tracing for microservices | [wiki](wiki/8-platform-mesh/Observability.md) |

### 7b. Databases

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **CloudNativePG** | PostgreSQL (CNCF Sandbox) | Automated failover, backup (Barman), connection pooling (PgBouncer) | [wiki](wiki/7-services/CloudNativePG.md) |
| **MySQL Operator** | MySQL | InnoDB Cluster, Group Replication, automated backup | [wiki](wiki/7-services/MySQL-Operator.md) |
| **MongoDB Operator** | MongoDB | Replica sets, automated scaling, backup | [wiki](wiki/7-services/MongoDB-Operator.md) |
| **Redis Operator** | Redis | Sentinel HA and Cluster mode, automatic failover | [wiki](wiki/7-services/Redis-Operator.md) |

### 7c. Messaging

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Strimzi** | Kafka (CNCF Sandbox) | Kafka clusters, topics, users, connectors, MirrorMaker | [wiki](wiki/7-services/Kafka-Operator.md) |
| **RabbitMQ Operator** | RabbitMQ | Cluster + Topology operators, queues, exchanges, bindings | [wiki](wiki/7-services/RabbitMQ-Operator.md) |

### 7d. Infrastructure Services

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **cert-manager** | TLS (CNCF Graduated) | Automated certificate lifecycle (Let's Encrypt, Vault, CA) | [wiki](wiki/7-services/Cert-Manager.md) |
| **External Secrets Operator** | Secrets sync | Bridge K8s secrets to external stores (Vault, AWS SM, Azure KV) | [wiki](wiki/8-platform-mesh/Secrets-Management.md) |

**Prerequisites:** Layer 4 (Kubernetes).
**Outcome:** Production-ready stateful services with automated lifecycle management.

---

## Layer 8 — Platform Mesh

### 8a. Core Platform Mesh

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **kcp** | Control plane | User-facing API layer — hierarchical workspaces, APIExport/APIBinding | [wiki](wiki/8-platform-mesh/User-Facing-Control-Plane.md) |
| **OpenFGA** | Authorization | Relationship-Based Access Control (ReBAC, Zanzibar-inspired) | [wiki](wiki/8-platform-mesh/Platform-Mesh-Security.md) |
| **Keycloak** | Identity | OIDC/OAuth2 identity provider, identity federation, per-org realms | [wiki](wiki/8-platform-mesh/Platform-Mesh-Security.md) |
| **Kratix** | Platform framework | Platform-as-a-Product — Promises (service contracts), Workflows (governance) | [wiki](wiki/8-platform-mesh/Kratix.md) |

### 8b. Security & Secrets

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **OpenBao** | Secrets / PKI | Secrets management, certificate lifecycle, HSM auto-unseal | [wiki](wiki/8-platform-mesh/Secrets-Management.md) |
| **OpenKCM** | Key management | Encryption key management — keychain hierarchy, BYOK/HYOK, HSM | [wiki](wiki/8-platform-mesh/Key-Management.md) |

**Prerequisites:** Layer 4 (Kubernetes), Layer 7 (cert-manager for TLS).
**Outcome:** Multi-tenant service marketplace with declarative service ordering, AuthN/AuthZ, and encrypted-at-rest data.

---

## Layer 9 — AI Agents

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **CAIPE Supervisor** | Multi-agent orchestrator | Coordinates specialized sub-agents via A2A protocol | [wiki](wiki/9-ai-agents/AI-Agents-Architecture.md) |
| **Platform Agents** | MCP agents | 14 agents: ArgoCD, GitHub, Jira, AWS, PagerDuty, Slack, Splunk, etc. | [wiki](wiki/9-ai-agents/AI-Platform-Agents.md) |
| **RAG Knowledge Base** | Knowledge system | Hybrid search (semantic + BM25), knowledge graph (Neo4j), MCP tools | [wiki](wiki/9-ai-agents/AI-Knowledge-Bases.md) |
| **Agentgateway** | Transport | Gateway between agents with OAuth-based agent identity | [wiki](wiki/9-ai-agents/AI-Agents-Architecture.md) |
| **openapi-mcp-codegen** | Code generator | Generate MCP servers from OpenAPI specs | [wiki](wiki/9-ai-agents/AI-Platform-Agents.md) |

**Prerequisites:** Layer 4 (Kubernetes), Layer 8 (Keycloak for OAuth), services to integrate with.
**Outcome:** AI-powered platform operations — incident response, deployment checks, cost analysis, PR reviews.

---

## Layer 10 — Portals

| Component | Type | Purpose | Docs |
|-----------|------|---------|------|
| **Backstage** | Developer portal (CNCF Graduated) | Software catalog, templates, TechDocs, plugin ecosystem (200+) | [wiki](wiki/10-portals/Backstage.md) |
| **OpenMFP** | Micro frontend platform | Runtime micro frontend composition, K8s-native (ContentConfiguration CRD) | [wiki](wiki/10-portals/OpenMFP-Portal.md) |
| **IDPBuilder** | IDP bootstrapper | Local IDP setup — ArgoCD + Backstage + Crossplane + Keycloak + Gitea | [wiki](wiki/10-portals/IDP-Reference-Implementation.md) |
| **Luigi** | MF framework | Micro frontend framework used by OpenMFP for composition | [wiki](wiki/10-portals/OpenMFP-Portal.md) |
| **CNOE CLI** | CLI tools | `cnoe template crd/tf` for Backstage template generation, `cnoe k8s verify` | [wiki](wiki/10-portals/CNOE-CLI.md) |

**Prerequisites:** Layer 4 (Kubernetes), Layer 8 (Keycloak, kcp), Layer 7 (services to display).
**Outcome:** Unified developer portal with self-service capabilities, service catalog, and documentation.

---

## Deployment Order Summary

| Phase | Layers | Duration Estimate | What You Get |
|-------|--------|-------------------|--------------|
| **Phase 1: Foundation** | 1 + 2 | — | Automated bare metal + IaaS |
| **Phase 2: Kubernetes** | 3 + 4a | — | Managed K8s clusters |
| **Phase 3: DevOps** | 4b + 4c + 4d | — | GitOps, IaC, policy enforcement |
| **Phase 4: Services** | 7 | — | Databases, messaging, monitoring |
| **Phase 5: Delivery** | 5 | — | Reproducible software delivery |
| **Phase 6: Platform** | 6 + 8 | — | Service mesh, security, marketplace |
| **Phase 7: Portal** | 10 | — | Developer self-service portal |
| **Phase 8: AI** | 9 | — | AI-powered platform operations |

> **Quick Start:** If starting from existing cloud infrastructure, skip Phases 1-2 and begin at Phase 2 (Layer 3). If you already have Kubernetes, start at Phase 3 (Layer 4b).

---

## Reference Stacks

| Stack | Components | Use Case |
|-------|------------|----------|
| **BACK Stack** | Backstage + ArgoCD + Crossplane + Kyverno | Minimal IDP |
| **CNOE Reference** | IDPBuilder + ArgoCD + Backstage + Crossplane + Keycloak + External Secrets | Full IDP demo |
| **ApeiroRA Showroom** | Gardener + Platform Mesh + OpenMFP + OpenFGA | Full Apeiro stack |
| **CAIPE** | Supervisor + 14 agents + RAG + Backstage | AI platform ops |
