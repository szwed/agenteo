# Observability

Apeiro uses **OpenTelemetry (OTel)** for telemetry. All components produce OTel-compatible data; no specific sink implementation imposed.

## Core Signals

- **Metrics** - numerical data points on system health over time (CPU, memory, latency)
- **Logs** - detailed records of events; structured/unstructured; used for auditing, troubleshooting
- **Traces** - follow request journeys through microservices; capture latency and failures

## Tools

- **Prometheus** - metrics collection and querying (time-series database)
- **OpenSearch** - scalable log indexing, search, and analysis
- **Jaeger** - distributed tracing across services

## Audit Logging

Captures audit-trail events for compliance. Subject to long retention periods with guaranteed completeness (delivery guarantee).

Requirements: durable WORM (write-once/read-many) storage (e.g. S3-compatible).

Work in progress with OpenTelemetry community:
- Semantic conventions for audit logs
- API/SDK extensions for audit logging
- Collector extensions for audit logging

## CNOE Perspective

CNOE emphasizes OpenTelemetry data collectors as the standard telemetry pipeline, with Prometheus for metrics collection and Grafana for visualization and analysis. This aligns directly with Apeiro's OTel-first approach -- both frameworks treat OTel as the universal telemetry substrate while remaining sink-agnostic. CNOE's reference implementations pair these with Argo-based CI/CD observability, reinforcing the pattern of unified observability across platform operations.

See also: [[Security]]
