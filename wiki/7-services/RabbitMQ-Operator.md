# RabbitMQ Operator

The **RabbitMQ Cluster Kubernetes Operator** is the official operator from VMware/Broadcom for managing RabbitMQ on Kubernetes.

## Overview

Deploys and manages RabbitMQ clusters declaratively. A companion Topology Operator manages queues, exchanges, bindings, and policies.

## CRDs

### Cluster Operator

| CRD | Purpose |
|---|---|
| `RabbitmqCluster` | RabbitMQ cluster deployment and configuration |

### Topology Operator

| CRD | Purpose |
|---|---|
| `Queue` | Queue declaration |
| `Exchange` | Exchange declaration |
| `Binding` | Binding between exchange and queue |
| `Policy` | RabbitMQ policy |
| `Vhost` | Virtual host management |
| `User` | User and permissions |

## Key Features

- Automated cluster deployment and scaling
- TLS encryption
- Persistent storage
- Prometheus metrics
- Topology management (queues, exchanges, bindings, policies) via dedicated operator
- Plugin management

## Links

- [GitHub — rabbitmq/cluster-operator](https://github.com/rabbitmq/cluster-operator)
- [GitHub — rabbitmq/messaging-topology-operator](https://github.com/rabbitmq/messaging-topology-operator)
