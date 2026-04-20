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

---

## Installation Steps

> **Assumption:** You have a running Kubernetes cluster (v1.27+), `kubectl` configured, and `helm` installed.
> All commands use default namespaces — adjust for production.

### Step 0 — Prerequisites

```bash
# Verify cluster access
kubectl cluster-info
kubectl get nodes

# Install Helm if not present
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# Add common Helm repos (used throughout)
helm repo add jetstack https://charts.jetstack.io
helm repo add argo https://argoproj.github.io/argo-helm
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add elastic https://helm.elastic.co
helm repo add strimzi https://strimzi.io/charts
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add cnpg https://cloudnative-pg.github.io/charts
helm repo add backstage https://backstage.github.io/charts
helm repo add keycloak https://codecentric.github.io/helm-charts
helm repo add kubevirt https://storage.googleapis.com/kubevirt-prow/devel/nightly/release/kubevirt/kubevirt
helm repo update
```

---

### Step 1 — cert-manager (TLS foundation)

Install first — many other components depend on it for TLS certificates.

```bash
# Install cert-manager with CRDs
helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager --create-namespace \
  --set crds.enabled=true

# Verify
kubectl wait --for=condition=Available deployment/cert-manager -n cert-manager --timeout=120s

# Create a self-signed ClusterIssuer (for dev/testing)
kubectl apply -f - <<EOF
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: selfsigned-issuer
spec:
  selfSigned: {}
EOF
```

---

### Step 2 — Argo CD (GitOps CD)

```bash
# Install Argo CD
helm install argocd argo/argo-cd \
  --namespace argocd --create-namespace \
  --set configs.params."server.insecure"=true

# Wait for ready
kubectl wait --for=condition=Available deployment/argocd-server -n argocd --timeout=180s

# Get initial admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

# Port-forward to access UI
kubectl port-forward svc/argocd-server -n argocd 8080:443 &
# Access at https://localhost:8080 (user: admin)
```

---

### Step 3 — Crossplane (Infrastructure as Code)

```bash
# Install Crossplane
helm install crossplane crossplane-stable/crossplane \
  --namespace crossplane-system --create-namespace

# Wait for ready
kubectl wait --for=condition=Available deployment/crossplane -n crossplane-system --timeout=120s

# Install AWS Provider (example — replace with your cloud)
kubectl apply -f - <<EOF
apiVersion: pkg.crossplane.io/v1
kind: Provider
metadata:
  name: provider-aws-s3
spec:
  package: xpkg.upbound.io/upbound/provider-aws-s3:v1.20.0
EOF

# For Azure: provider-family-azure
# For GCP: provider-family-gcp

# Configure credentials (example for AWS)
kubectl create secret generic aws-creds \
  -n crossplane-system \
  --from-file=creds=./aws-credentials.txt

kubectl apply -f - <<EOF
apiVersion: aws.upbound.io/v1beta1
kind: ProviderConfig
metadata:
  name: default
spec:
  credentials:
    source: Secret
    secretRef:
      namespace: crossplane-system
      name: aws-creds
      key: creds
EOF
```

---

### Step 4 — Kyverno (Policy Engine)

```bash
# Install Kyverno
helm install kyverno kyverno/kyverno \
  --namespace kyverno --create-namespace

helm repo add kyverno https://kyverno.github.io/kyverno/
helm repo update

helm install kyverno kyverno/kyverno \
  --namespace kyverno --create-namespace

# Wait for ready
kubectl wait --for=condition=Available deployment/kyverno-admission-controller -n kyverno --timeout=120s

# Example policy: require labels on all pods
kubectl apply -f - <<EOF
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: require-labels
spec:
  validationFailureAction: Audit
  rules:
  - name: check-team-label
    match:
      any:
      - resources:
          kinds:
          - Pod
    validate:
      message: "Label 'team' is required."
      pattern:
        metadata:
          labels:
            team: "?*"
EOF
```

---

### Step 5 — Prometheus Stack (Monitoring)

```bash
# Install kube-prometheus-stack (Prometheus + Alertmanager + Grafana)
helm install prometheus prometheus-community/kube-prometheus-stack \
  --namespace monitoring --create-namespace \
  --set grafana.adminPassword=admin

# Wait for ready
kubectl wait --for=condition=Available deployment/prometheus-grafana -n monitoring --timeout=180s

# Port-forward Grafana
kubectl port-forward svc/prometheus-grafana -n monitoring 3000:80 &
# Access at http://localhost:3000 (user: admin, password: admin)

# Port-forward Prometheus
kubectl port-forward svc/prometheus-kube-prometheus-prometheus -n monitoring 9090:9090 &
# Access at http://localhost:9090
```

---

### Step 6 — OpenTelemetry (Telemetry Collection)

```bash
# Install OpenTelemetry Operator
kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/latest/download/opentelemetry-operator.yaml

# Wait for operator
kubectl wait --for=condition=Available deployment/opentelemetry-operator-controller-manager \
  -n opentelemetry-operator-system --timeout=120s

# Deploy OTel Collector (sends to Prometheus)
kubectl apply -f - <<EOF
apiVersion: opentelemetry.io/v1beta1
kind: OpenTelemetryCollector
metadata:
  name: otel-collector
  namespace: monitoring
spec:
  mode: deployment
  config:
    receivers:
      otlp:
        protocols:
          grpc:
            endpoint: 0.0.0.0:4317
          http:
            endpoint: 0.0.0.0:4318
    exporters:
      prometheus:
        endpoint: 0.0.0.0:8889
    service:
      pipelines:
        metrics:
          receivers: [otlp]
          exporters: [prometheus]
EOF
```

---

### Step 7 — Elasticsearch / ECK (Log Analytics)

```bash
# Install ECK Operator
kubectl create -f https://download.elastic.co/downloads/eck/2.16.1/crds.yaml
kubectl apply -f https://download.elastic.co/downloads/eck/2.16.1/operator.yaml

# Wait for operator
kubectl wait --for=condition=Available deployment/elastic-operator -n elastic-system --timeout=120s

# Deploy Elasticsearch cluster
kubectl apply -f - <<EOF
apiVersion: elasticsearch.k8s.elastic.co/v1
kind: Elasticsearch
metadata:
  name: elasticsearch
  namespace: elastic-system
spec:
  version: 8.17.0
  nodeSets:
  - name: default
    count: 1
    config:
      node.store.allow_mmap: false
    podTemplate:
      spec:
        containers:
        - name: elasticsearch
          resources:
            requests:
              memory: 2Gi
            limits:
              memory: 2Gi
EOF

# Deploy Kibana
kubectl apply -f - <<EOF
apiVersion: kibana.k8s.elastic.co/v1
kind: Kibana
metadata:
  name: kibana
  namespace: elastic-system
spec:
  version: 8.17.0
  count: 1
  elasticsearchRef:
    name: elasticsearch
EOF

# Get Elasticsearch password
kubectl get secret elasticsearch-es-elastic-user -n elastic-system -o jsonpath='{.data.elastic}' | base64 -d && echo
```

---

### Step 8 — CloudNativePG (PostgreSQL)

```bash
# Install CloudNativePG operator
helm install cnpg cnpg/cloudnative-pg \
  --namespace cnpg-system --create-namespace

# Wait for ready
kubectl wait --for=condition=Available deployment/cnpg-cloudnative-pg -n cnpg-system --timeout=120s

# Deploy a PostgreSQL cluster
kubectl apply -f - <<EOF
apiVersion: postgresql.cnpg.io/v1
kind: Cluster
metadata:
  name: postgres-cluster
spec:
  instances: 3
  storage:
    size: 10Gi
  postgresql:
    parameters:
      shared_buffers: "256MB"
      max_connections: "100"
  bootstrap:
    initdb:
      database: appdb
      owner: appuser
EOF

# Get credentials
kubectl get secret postgres-cluster-app -o jsonpath='{.data.password}' | base64 -d && echo
```

---

### Step 9 — Redis Operator

```bash
# Install Redis Operator (OT-CONTAINER-KIT)
helm repo add ot-helm https://ot-container-kit.github.io/helm-charts/
helm install redis-operator ot-helm/redis-operator \
  --namespace redis-system --create-namespace

# Deploy Redis cluster
kubectl apply -f - <<EOF
apiVersion: redis.redis.opstreelabs.in/v1beta2
kind: RedisCluster
metadata:
  name: redis-cluster
spec:
  clusterSize: 3
  kubernetesConfig:
    image: quay.io/opstree/redis:v7.0.12
  storage:
    volumeClaimTemplate:
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
EOF
```

---

### Step 10 — Strimzi (Apache Kafka)

```bash
# Install Strimzi operator
helm install strimzi strimzi/strimzi-kafka-operator \
  --namespace kafka --create-namespace

# Wait for ready
kubectl wait --for=condition=Available deployment/strimzi-cluster-operator -n kafka --timeout=120s

# Deploy Kafka cluster
kubectl apply -f - <<EOF
apiVersion: kafka.strimzi.io/v1beta2
kind: Kafka
metadata:
  name: kafka-cluster
  namespace: kafka
spec:
  kafka:
    version: 3.9.0
    replicas: 3
    listeners:
      - name: plain
        port: 9092
        type: internal
        tls: false
    config:
      offsets.topic.replication.factor: 3
      transaction.state.log.replication.factor: 3
    storage:
      type: persistent-claim
      size: 10Gi
  zookeeper:
    replicas: 3
    storage:
      type: persistent-claim
      size: 5Gi
  entityOperator:
    topicOperator: {}
    userOperator: {}
EOF

# Create a test topic
kubectl apply -f - <<EOF
apiVersion: kafka.strimzi.io/v1beta2
kind: KafkaTopic
metadata:
  name: test-topic
  namespace: kafka
  labels:
    strimzi.io/cluster: kafka-cluster
spec:
  partitions: 3
  replicas: 3
EOF
```

---

### Step 11 — RabbitMQ Operator

```bash
# Install RabbitMQ Cluster Operator
kubectl apply -f https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml

# Deploy RabbitMQ cluster
kubectl apply -f - <<EOF
apiVersion: rabbitmq.com/v1beta1
kind: RabbitmqCluster
metadata:
  name: rabbitmq-cluster
spec:
  replicas: 3
  resources:
    requests:
      cpu: 500m
      memory: 1Gi
  persistence:
    storageClassName: standard
    storage: 5Gi
EOF

# Get default credentials
kubectl get secret rabbitmq-cluster-default-user -o jsonpath='{.data.username}' | base64 -d && echo
kubectl get secret rabbitmq-cluster-default-user -o jsonpath='{.data.password}' | base64 -d && echo
```

---

### Step 12 — Keycloak (Identity Provider)

```bash
# Install Keycloak
helm install keycloak keycloak/keycloakx \
  --namespace keycloak --create-namespace \
  --set command='{"/opt/keycloak/bin/kc.sh","start-dev"}' \
  --set extraEnv[0].name=KEYCLOAK_ADMIN \
  --set extraEnv[0].value=admin \
  --set extraEnv[1].name=KEYCLOAK_ADMIN_PASSWORD \
  --set extraEnv[1].value=admin \
  --set http.relativePath=/auth

# Wait for ready
kubectl wait --for=condition=Available deployment/keycloak-keycloakx -n keycloak --timeout=180s

# Port-forward
kubectl port-forward svc/keycloak-keycloakx-http -n keycloak 8081:80 &
# Access at http://localhost:8081/auth (user: admin, password: admin)
```

---

### Step 13 — External Secrets Operator

```bash
# Install External Secrets Operator
helm repo add external-secrets https://charts.external-secrets.io
helm install external-secrets external-secrets/external-secrets \
  --namespace external-secrets --create-namespace

# Wait for ready
kubectl wait --for=condition=Available deployment/external-secrets -n external-secrets --timeout=120s

# Example: connect to AWS Secrets Manager
kubectl apply -f - <<EOF
apiVersion: external-secrets.io/v1beta1
kind: SecretStore
metadata:
  name: aws-secrets
spec:
  provider:
    aws:
      service: SecretsManager
      region: eu-central-1
      auth:
        secretRef:
          accessKeyIDSecretRef:
            name: aws-creds
            key: access-key
          secretAccessKeySecretRef:
            name: aws-creds
            key: secret-key
EOF
```

---

### Step 14 — OpenBao (Secrets & PKI)

```bash
# Install OpenBao (Vault-compatible)
helm repo add openbao https://openbao.github.io/openbao-helm
helm install openbao openbao/openbao \
  --namespace openbao --create-namespace \
  --set server.dev.enabled=true

# Wait for ready
kubectl wait --for=condition=Ready pod/openbao-0 -n openbao --timeout=120s

# Port-forward
kubectl port-forward svc/openbao -n openbao 8200:8200 &
# Access at http://localhost:8200
```

---

### Step 15 — KubeVirt (Virtual Machines)

```bash
# Install KubeVirt operator
export KUBEVIRT_VERSION=$(curl -s https://api.github.com/repos/kubevirt/kubevirt/releases/latest | grep tag_name | cut -d '"' -f 4)

kubectl create -f "https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/kubevirt-operator.yaml"
kubectl create -f "https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/kubevirt-cr.yaml"

# Wait for ready
kubectl wait --for=condition=Available kubevirt/kubevirt -n kubevirt --timeout=300s

# Install virtctl CLI
curl -Lo virtctl "https://github.com/kubevirt/kubevirt/releases/download/${KUBEVIRT_VERSION}/virtctl-${KUBEVIRT_VERSION}-linux-amd64"
chmod +x virtctl && sudo mv virtctl /usr/local/bin/

# Test — create a VM
kubectl apply -f - <<EOF
apiVersion: kubevirt.io/v1
kind: VirtualMachine
metadata:
  name: test-vm
spec:
  running: false
  template:
    spec:
      domain:
        devices:
          disks:
          - name: containerdisk
            disk:
              bus: virtio
        resources:
          requests:
            memory: 128Mi
      volumes:
      - name: containerdisk
        containerDisk:
          image: quay.io/kubevirt/cirros-container-disk-demo
EOF

# Start the VM
virtctl start test-vm
```

---

### Step 16 — Backstage (Developer Portal)

```bash
# Create Backstage app
npx @backstage/create-app@latest --skip-install

cd backstage-app
yarn install
yarn tsc
yarn build

# Run locally for testing
yarn dev
# Access at http://localhost:3000

# For Kubernetes deployment, build Docker image:
yarn build-image --tag backstage:latest

# Deploy to cluster
kubectl create namespace backstage

kubectl apply -f - <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backstage
  namespace: backstage
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backstage
  template:
    metadata:
      labels:
        app: backstage
    spec:
      containers:
      - name: backstage
        image: backstage:latest
        ports:
        - containerPort: 7007
---
apiVersion: v1
kind: Service
metadata:
  name: backstage
  namespace: backstage
spec:
  selector:
    app: backstage
  ports:
  - port: 80
    targetPort: 7007
EOF

kubectl port-forward svc/backstage -n backstage 7007:80 &
# Access at http://localhost:7007
```

---

### Step 17 — CNOE IDPBuilder (All-in-One IDP)

Alternative to steps 2-16 for local development/demo — installs ArgoCD, Backstage, Crossplane, Keycloak, External Secrets in one command.

```bash
# Install IDPBuilder
curl -fsSL https://raw.githubusercontent.com/cnoe-io/idpbuilder/main/hack/install.sh | bash

# Create full reference IDP
idpbuilder create --use-path-routing \
  --package https://github.com/cnoe-io/stacks//ref-implementation

# Takes ~6 minutes. Access at:
# ArgoCD:         https://cnoe.localtest.me:8443/argocd
# Backstage:      https://cnoe.localtest.me:8443/
# Gitea:          https://cnoe.localtest.me:8443/gitea
# Keycloak:       https://cnoe.localtest.me:8443/keycloak
# Argo Workflows: https://cnoe.localtest.me:8443/argo-workflows

# Get credentials
idpbuilder get secrets
```

---

### Step 18 — CAIPE AI Agents

```bash
# Clone CAIPE
git clone https://github.com/cnoe-io/ai-platform-engineering.git
cd ai-platform-engineering

# Start with Docker Compose (recommended)
cp .env.example .env
# Edit .env — set your LLM API keys (OPENAI_API_KEY or ANTHROPIC_API_KEY)

docker compose -f docker-compose.dev.yaml up

# Access CAIPE UI at http://localhost:3000
# Supervisor A2A endpoint at http://localhost:8000

# Alternative: start individual components
# Supervisor
cd ai_platform_engineering && uv sync && uv run python -m supervisor

# UI
cd ui && npm install && npm run dev

# Knowledge Base (RAG)
cd ai_platform_engineering/knowledge_bases/rag
docker compose --profile apps up
# Web UI: http://localhost:9447
# MCP endpoint: http://localhost:9446/mcp
```

---

### Verification Checklist

After completing installation, verify each component:

```bash
echo "=== Cluster ===" && kubectl get nodes
echo "=== cert-manager ===" && kubectl get clusterissuer
echo "=== ArgoCD ===" && kubectl get applications -n argocd
echo "=== Crossplane ===" && kubectl get providers
echo "=== Kyverno ===" && kubectl get clusterpolicy
echo "=== Prometheus ===" && kubectl get prometheus -n monitoring
echo "=== OTel ===" && kubectl get opentelemetrycollectors -n monitoring
echo "=== ECK ===" && kubectl get elasticsearch -n elastic-system
echo "=== CloudNativePG ===" && kubectl get clusters.postgresql.cnpg.io
echo "=== Redis ===" && kubectl get rediscluster
echo "=== Kafka ===" && kubectl get kafka -n kafka
echo "=== RabbitMQ ===" && kubectl get rabbitmqcluster
echo "=== Keycloak ===" && kubectl get pods -n keycloak
echo "=== External Secrets ===" && kubectl get secretstores
echo "=== OpenBao ===" && kubectl get pods -n openbao
echo "=== KubeVirt ===" && kubectl get kubevirt -n kubevirt
echo "=== Backstage ===" && kubectl get pods -n backstage
```
