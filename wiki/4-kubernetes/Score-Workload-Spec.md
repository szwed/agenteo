# Score Workload Specification

Source: [score-spec/spec](https://github.com/score-spec/spec) (CNCF Sandbox)
Website: [score.dev](https://docs.score.dev/)

## What Is Score?

Score is a platform-agnostic, declarative workload specification. Developers describe **what their workload needs** (containers, databases, DNS, routes) in a single `score.yaml` file. A Score implementation then translates this into the target platform format (Docker Compose, Kubernetes manifests, Helm, etc.).

## Three Principles

1. **Platform-agnostic** — not tied to Docker, Kubernetes, or any specific tool. Define once, deploy anywhere.
2. **Tightly scoped** — describes workload-level properties only. Not a full YAML replacement for Kubernetes; shields developers from orchestrator complexity.
3. **Declarative** — developers state requirements; the platform resolves them. Establishes a contract: if requirements are honored, the workload runs as intended.

## Example

```yaml
apiVersion: score.dev/v1b1
metadata:
  name: sample

containers:
  main:
    image: ghcr.io/score-spec/sample-app:latest
    variables:
      PG_CONNECTION_STRING: "postgresql://${resources.db.username}:${resources.db.password}@${resources.db.host}:${resources.db.port}/${resources.db.database}"

service:
  ports:
    web:
      port: 8080

resources:
  db:
    type: postgres
  dns:
    type: dns
  route:
    type: route
    params:
      host: ${resources.dns.host}
      path: /
      port: 8080
```

Resources are declared by **type** (postgres, dns, route). The Score implementation links or provisions the actual backing service.

## Reference Implementations

| Implementation | Output |
|---|---|
| [score-compose](https://github.com/score-spec/score-compose) | `docker-compose.yaml` |
| [score-k8s](https://github.com/score-spec/score-k8s) | Kubernetes `manifests.yaml` |

Custom implementations can target Helm, Cloud Run, Nomad, or any platform.

## Benefits

- **Reduces cognitive load** — one spec instead of per-platform configs
- **Eliminates config drift** — single source of truth for workload requirements
- **Separates concerns** — environment-agnostic config (Score) vs environment-specific config (platform)
- **Faster onboarding** — developers learn one format, not Compose + Helm + Kustomize

## Relation to KRM

Score and [[KRM]] are complementary:

- **Score** targets the **developer experience** layer — what a workload needs, in platform-neutral terms
- **KRM** targets the **platform internals** layer — how resources are modeled, reconciled, and composed within Kubernetes

A platform team could accept Score files from developers and translate them into KRM resources for internal orchestration. Score sits above KRM in the abstraction stack.

## See Also

- [[KRM]] — Kubernetes Resource Model
- [[Developer-Portal]] — where developers might submit Score specs
- [[Platform-Mesh]] — the platform layer that resolves Score resource requirements
