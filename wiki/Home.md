# ApeiroRA Wiki

Obsidian wiki for the **Apeiro Reference Architecture** and related cloud-native platform engineering resources.

## Start Here

- [Apeiro Reference Architecture](Apeiro-Reference-Architecture.md) — overview and learning path
- [Architecture Overview](Architecture-Overview.md) — layered component view
- [Getting Started](Getting-Started.md) — entry points by infrastructure level

---

## Architecture Layers (bottom → top)

### 1. Bare Metal Automation

Physical server lifecycle management via Kubernetes principles.

- [Baremetal](1-bare-metal/Baremetal.md) — IronCore cloud-native server management
- [Operating Systems](1-bare-metal/Operating-Systems.md) — Garden Linux
- [Hardware Recommendations](1-bare-metal/Hardware-Recommendations.md) — control and work plane sizing
  - [Hardware Control Plane](1-bare-metal/Hardware-Control-Plane.md) — bare metal, CobaltCore, IronCore specs
  - [Hardware Work Plane](1-bare-metal/Hardware-Work-Plane.md) — compute, storage, network, AI training/inference
  - [Availability Zones and Scaling](1-bare-metal/Availability-Zones-and-Scaling.md) — multi-AZ and scaling options

### 2. Infrastructure Services

IaaS layer providing compute, network, and storage (IronCore, CobaltCore).

- [Showroom Scenarios](2-infrastructure-services/Showroom-Scenarios.md) — assembling Apeiro environments

### 3. Cluster Management

Managed Kubernetes and multi-cluster orchestration.

- [Managed Kubernetes as a Service](3-cluster-management/Managed-Kubernetes-as-a-Service.md) — Gardener (Garden/Seed/Shoot)
- [Cluster API](3-cluster-management/Cluster-API.md) — CAPI declarative cluster lifecycle
- [Multi Cluster Federation](3-cluster-management/Multi-Cluster-Federation.md) — centralized, agent-based, separated planes
- [Hosted Control Planes](3-cluster-management/Hosted-Control-Planes.md) — Kubeception pattern
- [Multi Cloud Service Provider](3-cluster-management/Multi-Cloud-Service-Provider.md) — servicelet pattern

### 4. Kubernetes

Core concepts, patterns, and tooling for Kubernetes-native platforms.

**Concepts:**
- [Digital Twins](4-kubernetes/Digital-Twins.md) — virtual representation of real-world systems
- [KRM](4-kubernetes/KRM.md) — Kubernetes Resource Model
  - [KRM Bi Directional](4-kubernetes/KRM-Bi-Directional.md) / [KRM Control](4-kubernetes/KRM-Control.md) / [KRM Format](4-kubernetes/KRM-Format.md) / [KRM Kubernetes](4-kubernetes/KRM-Kubernetes.md)
- [Controller Pattern](4-kubernetes/Controller-Pattern.md) — reconciliation, PID analogy, edge/level triggering
- [Controller Archetypes](4-kubernetes/Controller-Archetypes.md) — actuator, attribute, aspect, logical object
- [Digital Twins Extensibility](4-kubernetes/Digital-Twins-Extensibility.md) — CRDs, Extension API Server

**Architecture:**
- [Control Data Work Planes](4-kubernetes/Control-Data-Work-Planes.md) — three-plane model
- [Kubernetes Implementation Design](4-kubernetes/Kubernetes-Implementation-Design.md) — K8s planes implementation
- [Multi Plane Controller](4-kubernetes/Multi-Plane-Controller.md) — multi-control-plane aware controllers
- [Data and Control Plane State](4-kubernetes/Data-and-Control-Plane-State.md) — backup, migration, pivoting

**Tooling:**
- [Crossplane](4-kubernetes/Crossplane.md) — Kubernetes-native IaC (CNCF Graduated)
- [Infrastructure as Code](4-kubernetes/Infrastructure-as-Code.md) — Terraform vs Crossplane, occasionally vs continuously reconciled
- [KubeVirt](4-kubernetes/KubeVirt.md) — virtual machines on Kubernetes
- [Score Workload Spec](4-kubernetes/Score-Workload-Spec.md) — platform-agnostic workload specification (CNCF Sandbox)

**DevOps:**
- [CI CD](4-kubernetes/CI-CD.md) — GitOps (ArgoCD, Flux), CI (Argo Workflows, Tekton)
- [GitOps and Repositories](4-kubernetes/GitOps-and-Repositories.md) — code repos, config repos, GitOps pattern
- [Validation and Policy](4-kubernetes/Validation-and-Policy.md) — admission control, OPA, Kyverno
- [Service Discovery](4-kubernetes/Service-Discovery.md) — DNS, registries, bootstrapping
- [Signing and Supply Chain](4-kubernetes/Signing-and-Supply-Chain.md) — cryptographic signing, attestations, SSSC

**Reference:**
- [CNCF Operator White Paper](4-kubernetes/CNCF-Operator-White-Paper.md) — operator taxonomy and best practices

### 5. Software Delivery

Application lifecycle, packaging, and deployment.

- [Lifecycle Management](5-software-delivery/Lifecycle-Management.md) — LCM overview
  - [LCM Operator Installation](5-software-delivery/LCM-Operator-Installation.md) — operator-based install/update (4 principles)
  - [Software Bill of Delivery](5-software-delivery/Software-Bill-of-Delivery.md) — OCM as SBoD, release channels
- [Konfidence](5-software-delivery/Konfidence.md) — SaaS delivery framework (immutable vectors, ring deployments)
  - [Konfidence Core Concepts](5-software-delivery/Konfidence-Core-Concepts.md) — artifact, vector, stage, landscape
- [Micro Frontends](5-software-delivery/Micro-Frontends.md) — architectural pattern for composable UIs
  - [OpenMFP](5-software-delivery/OpenMFP.md) — Apeiro's micro frontend integration

### 6. Data Fabric

Metadata-driven data integration and discovery.

- [Data Fabric](6-data-fabric/Data-Fabric.md) — architectural approach, key elements
  - [Data Fabric Perspectives](6-data-fabric/Data-Fabric-Perspectives.md) — developer, integrator, analyst, service supplier
  - [Data Fabric Principles](6-data-fabric/Data-Fabric-Principles.md) — self-descriptive, discoverable, aligned metadata
  - [Data Fabric Components](6-data-fabric/Data-Fabric-Components.md) — ORD, UMS, aligned metadata model
  - [Data Fabric Landscape](6-data-fabric/Data-Fabric-Landscape.md) — metadata flow and visualization

### 7. Services

Kubernetes operators for managing stateful services and third-party applications.

- [Services Overview](7-services/Services-Overview.md) — operator pattern for managed services

**Observability:**
- [Prometheus Operator](7-services/Prometheus-Operator.md) — metrics, alerting, Grafana
- [Elasticsearch Operator](7-services/Elasticsearch-Operator.md) — ECK (Elasticsearch, Kibana, APM)

**Databases:**
- [CloudNativePG](7-services/CloudNativePG.md) — PostgreSQL (CNCF Sandbox)
- [MySQL Operator](7-services/MySQL-Operator.md) — MySQL InnoDB Cluster
- [MongoDB Operator](7-services/MongoDB-Operator.md) — MongoDB replica sets
- [Redis Operator](7-services/Redis-Operator.md) — Redis Sentinel and Cluster

**Messaging:**
- [Kafka Operator](7-services/Kafka-Operator.md) — Strimzi for Apache Kafka (CNCF Sandbox)
- [RabbitMQ Operator](7-services/RabbitMQ-Operator.md) — RabbitMQ clusters

**Infrastructure:**
- [Cert Manager](7-services/Cert-Manager.md) — TLS certificate automation (CNCF Graduated)
- [ArgoCD Operator](7-services/ArgoCD-Operator.md) — ArgoCD GitOps engine

### 8. Platform Mesh

Service orchestration, security, and marketplace across the cloud-edge continuum.

**Core:**
- [Platform Mesh](8-platform-mesh/Platform-Mesh.md) — service providers and consumers
- [Platform Mesh Perspectives](8-platform-mesh/Platform-Mesh-Perspectives.md) — developer, supplier, operator
- [Platform Mesh Design Goals](8-platform-mesh/Platform-Mesh-Design-Goals.md) — service orchestration environment
- [Platform Mesh Guiding Principles](8-platform-mesh/Platform-Mesh-Guiding-Principles.md) — declarative API, decoupling
- [Platform Mesh Design Decisions](8-platform-mesh/Platform-Mesh-Design-Decisions.md) — MSP pattern, uniform KRM API

**Components:**
- [Service Provider Control Planes](8-platform-mesh/Service-Provider-Control-Planes.md) — KRM-based lifecycle management
- [Platform Mesh Account Model](8-platform-mesh/Platform-Mesh-Account-Model.md) — hierarchical accounts via kcp
- [User Facing Control Plane](8-platform-mesh/User-Facing-Control-Plane.md) — kcp workspaces, APIExport/APIBinding

**Service Model:**
- [Service Concepts](8-platform-mesh/Service-Concepts.md) — service, capability, resource, provider definitions
- [Managed Service Provider Pattern](8-platform-mesh/Managed-Service-Provider-Pattern.md) — coordinator + servicelet
- [Kratix](8-platform-mesh/Kratix.md) — platform-as-a-product framework (Promises, Workflows)

**Security & Observability:**
- [Platform Mesh Security](8-platform-mesh/Platform-Mesh-Security.md) — AuthN (Keycloak/OIDC) + AuthZ (RBAC + OpenFGA)
- [Security](8-platform-mesh/Security.md) — overview linking sub-topics
  - [Security Compliance Automation](8-platform-mesh/Security-Compliance-Automation.md) — SCF, OCM coordinates
  - [Key Management](8-platform-mesh/Key-Management.md) — OpenKCM, HSM, keychain hierarchy
  - [Secrets Management](8-platform-mesh/Secrets-Management.md) — OpenBao, PKI, ACME
- [Observability](8-platform-mesh/Observability.md) — OpenTelemetry, audit logging

### 9. AI Agents

Multi-agent AI systems for platform engineering automation.

- [AI Agents Overview](9-ai-agents/AI-Agents-Overview.md) — Community AI Platform Engineering
- [AI Agents Architecture](9-ai-agents/AI-Agents-Architecture.md) — 6-stage evolution (ReAct → enterprise)
- [AI Platform Agents](9-ai-agents/AI-Platform-Agents.md) — 14 platform agents (ArgoCD, GitHub, Jira, AWS, etc.)
- [AI Knowledge Bases](9-ai-agents/AI-Knowledge-Bases.md) — RAG hybrid search, knowledge graph, ontology
- [AI Prompt Library](9-ai-agents/AI-Prompt-Library.md) — basic and deep agent prompt configurations
- [AI Agents Security](9-ai-agents/AI-Agents-Security.md) — OAuth, A2A protocol, policy enforcement
- [AI Use Cases](9-ai-agents/AI-Use-Cases.md) — personas, pre-built skills
- [AI Agents UI](9-ai-agents/AI-Agents-UI.md) — A2A Message Visualizer (Next.js)

### 10. Portals

Developer portals and micro frontend platforms.

**Concepts:**
- [Portals Overview](10-portals/Portals-Overview.md) — comparing Backstage and OpenMFP approaches
- [Developer Portal](10-portals/Developer-Portal.md) — IDP portal concepts and requirements

**Backstage (CNCF):**
- [Backstage](10-portals/Backstage.md) — software catalog, templates, TechDocs, plugins
- [Backstage Plugins](10-portals/Backstage-Plugins.md) — CNOE-developed Backstage plugins

**OpenMFP (Apeiro):**
- [OpenMFP Portal](10-portals/OpenMFP-Portal.md) — micro frontend runtime composition, K8s-native

**CNOE IDP Reference:**
- [IDP Reference Implementation](10-portals/IDP-Reference-Implementation.md) — IDPBuilder reference stack
  - [IDPBuilder Details](10-portals/IDPBuilder-Details.md) — networking, certificates, OCI registry
  - [IDPBuilder Stacks](10-portals/IDPBuilder-Stacks.md) — available community stacks
- [CNOE CLI](10-portals/CNOE-CLI.md) — template generation and verification tools

---

## Resources

- [Resources Documents](Resources-Documents.md) — slides, blueprints, IPCEI-CIS documents
- [Resources Conferences](Resources-Conferences.md) — conference talks and recordings

## Cross-Cutting

- [CNOE](CNOE.md) — Cloud Native Operational Excellence framework
- [CNOE Technology Choices](CNOE-Technology-Choices.md) — capability-to-technology mapping
- [CNCF Platforms White Paper](CNCF-Platforms-White-Paper.md) — CNCF definition of internal platforms
- [Platform Maturity Model](Platform-Maturity-Model.md) — 5-dimension maturity assessment
- [BACK Stack](BACK-Stack.md) — Backstage + ArgoCD + Crossplane + Kyverno reference
