# KRM Control through Choreography

Multiple controllers with independent reconciliation loops collaborate to produce emergent behavior greater than the sum of parts.

## Orchestration vs Choreography

**Orchestration**: central supervisor directs flow. Simpler, observable, but introduces tight coupling, rigidity, single point of failure. Mitigated by durable execution workflows or SAGA pattern.

**Choreography**: components manage functions autonomously, contributing to emergent behavior. Decentralized, resilient, loosely coupled. Relies on message broker (or API server). Harder to reason about holistically.

Kubernetes uses **choreography** but can incorporate orchestration benefits.

## The "Invisible Hand"

Kubernetes motivates individual controllers acting in self-interest (each catering to a specific concern) to produce desired overall system behavior -- analogous to Adam Smith's invisible hand in economics. Proven more robust than centralized systems.
