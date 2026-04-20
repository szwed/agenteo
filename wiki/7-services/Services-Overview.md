# Services Overview

Kubernetes operators for managing stateful services and third-party applications on Kubernetes clusters.

The operator pattern (see [Controller Pattern](../4-kubernetes/Controller-Pattern.md), [CNCF Operator White Paper](../4-kubernetes/CNCF-Operator-White-Paper.md)) enables automated lifecycle management of complex applications — provisioning, scaling, backup, failover, and upgrades — through custom controllers and CRDs.

## Service Categories

### Observability
- [Prometheus Operator](Prometheus-Operator.md) — metrics, alerting, dashboards
- [Elasticsearch Operator](Elasticsearch-Operator.md) — log aggregation, search, APM

### Databases
- [CloudNativePG](CloudNativePG.md) — PostgreSQL
- [MySQL Operator](MySQL-Operator.md) — MySQL / InnoDB Cluster
- [MongoDB Operator](MongoDB-Operator.md) — MongoDB replica sets
- [Redis Operator](Redis-Operator.md) — Redis Sentinel and Cluster

### Messaging
- [Kafka Operator](Kafka-Operator.md) — Apache Kafka (Strimzi)
- [RabbitMQ Operator](RabbitMQ-Operator.md) — RabbitMQ clusters

### Infrastructure Services
- [Cert Manager](Cert-Manager.md) — TLS certificate management
- [ArgoCD Operator](ArgoCD-Operator.md) — GitOps continuous delivery

### Virtualization
- [KubeVirt](../4-kubernetes/KubeVirt.md) — virtual machines on Kubernetes
