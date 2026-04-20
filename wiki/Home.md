# ApeiroRA Wiki

Obsidian wiki for the **Apeiro Reference Architecture** and related cloud-native platform engineering resources.

## Start Here

- [[Apeiro-Reference-Architecture]] — overview and learning path
- [[Architecture-Overview]] — layered component view
- [[Getting-Started]] — entry points by infrastructure level

---

## Architecture Layers (bottom → top)

### 1. Bare Metal Automation

Physical server lifecycle management via Kubernetes principles.

- [[Baremetal]] — IronCore cloud-native server management
- [[Operating-Systems]] — Garden Linux
- [[Hardware-Recommendations]] — control and work plane sizing
  - [[Hardware-Control-Plane]] — bare metal, CobaltCore, IronCore specs
  - [[Hardware-Work-Plane]] — compute, storage, network, AI training/inference
  - [[Availability-Zones-and-Scaling]] — multi-AZ and scaling options

### 2. Infrastructure Services

IaaS layer providing compute, network, and storage (IronCore, CobaltCore).

- [[Showroom-Scenarios]] — assembling Apeiro environments

### 3. Cluster Management

Managed Kubernetes and multi-cluster orchestration.

- [[Managed-Kubernetes-as-a-Service]] — Gardener (Garden/Seed/Shoot)
- [[Cluster-API]] — CAPI declarative cluster lifecycle
- [[Multi-Cluster-Federation]] — centralized, agent-based, separated planes
- [[Hosted-Control-Planes]] — Kubeception pattern
- [[Multi-Cloud-Service-Provider]] — servicelet pattern

### 4. Kubernetes

Core concepts, patterns, and tooling for Kubernetes-native platforms.

**Concepts:**
- [[Digital-Twins]] — virtual representation of real-world systems
- [[KRM]] — Kubernetes Resource Model
  - [[KRM-Bi-Directional]] / [[KRM-Control]] / [[KRM-Format]] / [[KRM-Kubernetes]]
- [[Controller-Pattern]] — reconciliation, PID analogy, edge/level triggering
- [[Controller-Archetypes]] — actuator, attribute, aspect, logical object
- [[Digital-Twins-Extensibility]] — CRDs, Extension API Server

**Architecture:**
- [[Control-Data-Work-Planes]] — three-plane model
- [[Kubernetes-Implementation-Design]] — K8s planes implementation
- [[Multi-Plane-Controller]] — multi-control-plane aware controllers
- [[Data-and-Control-Plane-State]] — backup, migration, pivoting

**Tooling:**
- [[Crossplane]] — Kubernetes-native IaC (CNCF Graduated)
- [[Infrastructure-as-Code]] — Terraform vs Crossplane, occasionally vs continuously reconciled
- [[KubeVirt]] — virtual machines on Kubernetes
- [[Score-Workload-Spec]] — platform-agnostic workload specification (CNCF Sandbox)

**DevOps:**
- [[CI-CD]] — GitOps (ArgoCD, Flux), CI (Argo Workflows, Tekton)
- [[GitOps-and-Repositories]] — code repos, config repos, GitOps pattern
- [[Validation-and-Policy]] — admission control, OPA, Kyverno
- [[Service-Discovery]] — DNS, registries, bootstrapping
- [[Signing-and-Supply-Chain]] — cryptographic signing, attestations, SSSC

**Reference:**
- [[CNCF-Operator-White-Paper]] — operator taxonomy and best practices

### 5. Software Delivery

Application lifecycle, packaging, and deployment.

- [[Lifecycle-Management]] — LCM overview
  - [[LCM-Operator-Installation]] — operator-based install/update (4 principles)
  - [[Software-Bill-of-Delivery]] — OCM as SBoD, release channels
- [[Konfidence]] — SaaS delivery framework (immutable vectors, ring deployments)
  - [[Konfidence-Core-Concepts]] — artifact, vector, stage, landscape
- [[Micro-Frontends]] — architectural pattern for composable UIs
  - [[OpenMFP]] — Apeiro's micro frontend integration

### 6. Data Fabric

Metadata-driven data integration and discovery.

- [[Data-Fabric]] — architectural approach, key elements
  - [[Data-Fabric-Perspectives]] — developer, integrator, analyst, service supplier
  - [[Data-Fabric-Principles]] — self-descriptive, discoverable, aligned metadata
  - [[Data-Fabric-Components]] — ORD, UMS, aligned metadata model
  - [[Data-Fabric-Landscape]] — metadata flow and visualization

### 7. Services

Kubernetes operators for managing stateful services and third-party applications.

- [[Services-Overview]] — operator pattern for managed services

**Observability:**
- [[Prometheus-Operator]] — metrics, alerting, Grafana
- [[Elasticsearch-Operator]] — ECK (Elasticsearch, Kibana, APM)

**Databases:**
- [[CloudNativePG]] — PostgreSQL (CNCF Sandbox)
- [[MySQL-Operator]] — MySQL InnoDB Cluster
- [[MongoDB-Operator]] — MongoDB replica sets
- [[Redis-Operator]] — Redis Sentinel and Cluster

**Messaging:**
- [[Kafka-Operator]] — Strimzi for Apache Kafka (CNCF Sandbox)
- [[RabbitMQ-Operator]] — RabbitMQ clusters

**Infrastructure:**
- [[Cert-Manager]] — TLS certificate automation (CNCF Graduated)
- [[ArgoCD-Operator]] — ArgoCD GitOps engine

### 8. Platform Mesh

Service orchestration, security, and marketplace across the cloud-edge continuum.

**Core:**
- [[Platform-Mesh]] — service providers and consumers
- [[Platform-Mesh-Perspectives]] — developer, supplier, operator
- [[Platform-Mesh-Design-Goals]] — service orchestration environment
- [[Platform-Mesh-Guiding-Principles]] — declarative API, decoupling
- [[Platform-Mesh-Design-Decisions]] — MSP pattern, uniform KRM API

**Components:**
- [[Service-Provider-Control-Planes]] — KRM-based lifecycle management
- [[Platform-Mesh-Account-Model]] — hierarchical accounts via kcp
- [[User-Facing-Control-Plane]] — kcp workspaces, APIExport/APIBinding

**Service Model:**
- [[Service-Concepts]] — service, capability, resource, provider definitions
- [[Managed-Service-Provider-Pattern]] — coordinator + servicelet
- [[Kratix]] — platform-as-a-product framework (Promises, Workflows)

**Security & Observability:**
- [[Platform-Mesh-Security]] — AuthN (Keycloak/OIDC) + AuthZ (RBAC + OpenFGA)
- [[Security]] — overview linking sub-topics
  - [[Security-Compliance-Automation]] — SCF, OCM coordinates
  - [[Key-Management]] — OpenKCM, HSM, keychain hierarchy
  - [[Secrets-Management]] — OpenBao, PKI, ACME
- [[Observability]] — OpenTelemetry, audit logging

### 9. AI Agents

Multi-agent AI systems for platform engineering automation.

- [[AI-Agents-Overview]] — Community AI Platform Engineering
- [[AI-Agents-Architecture]] — 6-stage evolution (ReAct → enterprise)
- [[AI-Platform-Agents]] — 14 platform agents (ArgoCD, GitHub, Jira, AWS, etc.)
- [[AI-Knowledge-Bases]] — RAG hybrid search, knowledge graph, ontology
- [[AI-Prompt-Library]] — basic and deep agent prompt configurations
- [[AI-Agents-Security]] — OAuth, A2A protocol, policy enforcement
- [[AI-Use-Cases]] — personas, pre-built skills
- [[AI-Agents-UI]] — A2A Message Visualizer (Next.js)

### 10. Portals

Developer portals and micro frontend platforms.

**Concepts:**
- [[Portals-Overview]] — comparing Backstage and OpenMFP approaches
- [[Developer-Portal]] — IDP portal concepts and requirements

**Backstage (CNCF):**
- [[Backstage]] — software catalog, templates, TechDocs, plugins
- [[Backstage-Plugins]] — CNOE-developed Backstage plugins

**OpenMFP (Apeiro):**
- [[OpenMFP-Portal]] — micro frontend runtime composition, K8s-native

**CNOE IDP Reference:**
- [[IDP-Reference-Implementation]] — IDPBuilder reference stack
  - [[IDPBuilder-Details]] — networking, certificates, OCI registry
  - [[IDPBuilder-Stacks]] — available community stacks
- [[CNOE-CLI]] — template generation and verification tools

---

## Resources

- [[Resources-Documents]] — slides, blueprints, IPCEI-CIS documents
- [[Resources-Conferences]] — conference talks and recordings

## Cross-Cutting

- [[CNOE]] — Cloud Native Operational Excellence framework
- [[CNOE-Technology-Choices]] — capability-to-technology mapping
- [[CNCF-Platforms-White-Paper]] — CNCF definition of internal platforms
- [[Platform-Maturity-Model]] — 5-dimension maturity assessment
- [[BACK-Stack]] — Backstage + ArgoCD + Crossplane + Kyverno reference
