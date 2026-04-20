# Controller Pattern

[KRM](KRM.md) is tightly coupled with the controller pattern: observed state is continuously reconciled with desired state; processed state is asynchronously reported back.

## PID Controller Analogy

The pattern maps to a PID (Proportional-Integral-Derivative) controller:

- **P (Proportional)** -- immediate response to discrepancy between desired and actual state
- **I (Integral)** -- accumulated past errors over time (e.g., `CrashLoopBackOff`, historical load scaling)
- **D (Derivative)** -- predicted future behavior based on rate of change (e.g., scaling on predicted demand)
- **Reconciliation** -- continuous correction to minimize error, tuned to avoid oscillation
- **Feedback** -- from shared repository of resources and actual state via API server
- **Self-healing** -- automatic adjustment at micro level; immutable infrastructure at macro level

## Edge vs Level Triggering

**Edge triggering**: react to specific events/changes. Efficient but less resilient to missed events.

**Level triggering**: continuously monitor actual vs desired state. Resilient but resource-intensive.

**Hybrid approach** (common in practice): `ReplicaSet` uses level-based reconciliation for replica count but edge-triggers on Pod deletion for fast failure response.
