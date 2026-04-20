# Elasticsearch Operator (ECK)

**Elastic Cloud on Kubernetes (ECK)** is the official Elastic operator for deploying and managing the Elastic Stack on Kubernetes.

## Overview

Manages Elasticsearch clusters and related components (Kibana, APM, Fleet, Beats) declaratively on Kubernetes.

## CRDs

| CRD | Purpose |
|---|---|
| `Elasticsearch` | Elasticsearch cluster (node roles, storage, scaling) |
| `Kibana` | Kibana instance linked to an Elasticsearch cluster |
| `ApmServer` | APM Server for application performance monitoring |
| `Agent` | Elastic Agent / Fleet Server |
| `Beat` | Filebeat, Metricbeat, etc. |
| `EnterpriseSearch` | Enterprise Search instance |
| `ElasticMapsServer` | Maps service |

## Key Features

- Multi-node clusters with configurable node roles
- Rolling upgrades with zero downtime
- Automatic TLS certificate management
- Snapshot and restore to object storage
- Autoscaling based on storage and memory
- Secure by default (TLS, RBAC)

Part of the [[Observability]] stack.

## Links

- [GitHub — elastic/cloud-on-k8s](https://github.com/elastic/cloud-on-k8s)
- [ECK Documentation](https://www.elastic.co/guide/en/cloud-on-k8s/current/index.html)
