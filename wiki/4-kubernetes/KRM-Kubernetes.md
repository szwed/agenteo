# KRM in Kubernetes

`kubectl api-resources` lists all [[Digital-Twins|digital twin]] types that Kubernetes supports as container orchestrator.

## Resource Attributes

Each resource type exposes:
- **Name** -- used in kubectl commands
- **Shortnames** -- abbreviated aliases
- **APIversion** -- API group and version (e.g., `v1`, `apps/v1`)
- **Namespaced** -- scoped to namespace (true) or cluster-wide (false)
- **Kind** -- semantic type

## Skills Portability

Familiarity with Kubernetes allows developers and administrators to apply and convert skills toward other capabilities modeled with [[KRM]].
