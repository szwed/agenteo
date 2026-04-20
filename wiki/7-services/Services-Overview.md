# Services Overview

Kubernetes operators for managing stateful services and third-party applications on Kubernetes clusters.

The operator pattern (see [[Controller-Pattern]], [[CNCF-Operator-White-Paper]]) enables automated lifecycle management of complex applications — provisioning, scaling, backup, failover, and upgrades — through custom controllers and CRDs.

## Service Categories

### Observability
- [[Prometheus-Operator]] — metrics, alerting, dashboards
- [[Elasticsearch-Operator]] — log aggregation, search, APM

### Databases
- [[CloudNativePG]] — PostgreSQL
- [[MySQL-Operator]] — MySQL / InnoDB Cluster
- [[MongoDB-Operator]] — MongoDB replica sets
- [[Redis-Operator]] — Redis Sentinel and Cluster

### Messaging
- [[Kafka-Operator]] — Apache Kafka (Strimzi)
- [[RabbitMQ-Operator]] — RabbitMQ clusters

### Infrastructure Services
- [[Cert-Manager]] — TLS certificate management
- [[ArgoCD-Operator]] — GitOps continuous delivery

### Virtualization
- [[KubeVirt]] — virtual machines on Kubernetes
