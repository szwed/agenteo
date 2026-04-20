# Prometheus Operator

The **Prometheus Operator** (and the **kube-prometheus-stack** Helm chart) provides Kubernetes-native deployment and management of Prometheus, Alertmanager, and Grafana.

## Overview

Defines monitoring infrastructure declaratively via CRDs. Part of the [Observability](../8-platform-mesh/Observability.md) stack. The operator watches for changes to these custom resources and reconciles the desired monitoring configuration.

## CRDs

| CRD | Purpose |
|---|---|
| `Prometheus` | Defines a Prometheus server instance |
| `ServiceMonitor` | Declares which Services to scrape |
| `PodMonitor` | Declares which Pods to scrape directly |
| `AlertmanagerConfig` | Alertmanager routing and receivers |
| `PrometheusRule` | Recording and alerting rules |
| `ThanosRuler` | Thanos rule evaluation |

## Key Features

- Automatic target discovery via ServiceMonitor/PodMonitor
- Prometheus and Alertmanager cluster management
- Persistent storage, sharding, high availability
- kube-prometheus-stack bundles Grafana dashboards and default alerts

## Links

- [GitHub — prometheus-operator/prometheus-operator](https://github.com/prometheus-operator/prometheus-operator)
- [kube-prometheus-stack Helm chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)
