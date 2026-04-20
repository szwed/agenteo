# CloudNativePG

**CloudNativePG** is a CNCF Sandbox project — a Kubernetes operator for managing PostgreSQL clusters natively on Kubernetes.

## Overview

Designed from the ground up for Kubernetes. No external tools required — manages the full PostgreSQL lifecycle declaratively.

## Key Features

- Declarative cluster management (primary + replicas)
- Automated failover and switchover
- Backup and restore via Barman (object storage: S3, GCS, Azure)
- Rolling updates with zero downtime
- Connection pooling via PgBouncer integration
- Monitoring with Prometheus metrics
- TLS encryption and certificate management

## CRDs

| CRD | Purpose |
|---|---|
| `Cluster` | PostgreSQL cluster definition (instances, storage, backup) |
| `Backup` | On-demand backup request |
| `ScheduledBackup` | Cron-based backup schedule |
| `Pooler` | PgBouncer connection pooler |

## Links

- [cloudnative-pg.io](https://cloudnative-pg.io/)
- [GitHub — cloudnative-pg/cloudnative-pg](https://github.com/cloudnative-pg/cloudnative-pg)
