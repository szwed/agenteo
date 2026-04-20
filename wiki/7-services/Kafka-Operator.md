# Kafka Operator (Strimzi)

**Strimzi** is a CNCF Sandbox project for running Apache Kafka on Kubernetes.

## Overview

Provides a Kubernetes-native way to run Kafka clusters, manage topics, users, and connectors declaratively.

## CRDs

| CRD | Purpose |
|---|---|
| `Kafka` | Kafka cluster (brokers, ZooKeeper/KRaft, listeners) |
| `KafkaTopic` | Topic management (partitions, replicas, config) |
| `KafkaUser` | User authentication and ACLs |
| `KafkaConnect` | Kafka Connect cluster for connectors |
| `KafkaMirrorMaker2` | Cross-cluster replication |
| `KafkaBridge` | HTTP bridge for Kafka |
| `KafkaRebalance` | Cruise Control rebalancing |

## Key Features

- KRaft mode (ZooKeeper-less) and ZooKeeper-based clusters
- Rack awareness for fault tolerance
- Cruise Control integration for partition rebalancing
- OAuth 2.0 authentication, TLS encryption
- Kafka Connect with build support for connector plugins
- Cross-datacenter replication via MirrorMaker 2

## Links

- [strimzi.io](https://strimzi.io/)
- [GitHub — strimzi/strimzi-kafka-operator](https://github.com/strimzi/strimzi-kafka-operator)
