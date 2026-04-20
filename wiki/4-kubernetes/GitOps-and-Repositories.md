# GitOps and Repositories

GitOps treats Git as the single source of truth for both application code and infrastructure configuration. CNOE identifies code repositories and config repositories as distinct capabilities, connected by reconciling controllers (ArgoCD, Flux) that close the loop between desired and actual state.

## Code Repositories

Code repositories store application source and are optimized for collaborative development.

**Characteristics:**
- Git-based version control
- Branching, pull requests, code review
- Change control and audit trail
- CI triggers (build, test, scan on push/PR)

In the CNOE reference implementation, Gitea serves as the in-cluster Git server. In production, organizations typically use GitHub, GitLab, or Bitbucket.

## Config Repositories

Config repositories store deployment configuration -- the desired state of what should be running where.

**Characteristics:**
- **Key-value and hierarchical** -- Configuration organized by environment, region, cluster
- **Versioned** -- Every change is a Git commit with author, timestamp, message
- **Immutable history** -- Git log provides complete audit trail
- **No secrets** -- Secrets belong in secret stores (Vault, KMS), referenced by config but never stored in Git. See [[Secrets-Management]].

Config repos contain [[KRM-Format]] manifests (YAML), Helm charts, Kustomize overlays, or Crossplane claims. These are the "at-rest" representations of desired state.

## GitOps as a Pattern

GitOps connects code and config repos to the cluster through reconciling controllers:

1. Developer pushes code to code repo
2. CI pipeline (Argo Workflows, Tekton) builds, tests, produces artifacts
3. CI updates config repo (new image tag, updated manifest)
4. CD controller (ArgoCD, Flux) detects config change
5. CD controller reconciles cluster state to match config repo

The reconciliation is continuous -- not a one-time deploy. If someone manually changes a resource in the cluster, the controller reverts it to match Git. This is the same [[Controller-Pattern]] that drives [[Digital-Twins]] and [[Infrastructure-as-Code]].

```
Code Repo --> [CI: build/test] --> Config Repo --> [CD: reconcile] --> Cluster
                                       ^                                  |
                                       |--- drift detection --------------|
```

## Separation of Concerns

Keeping code and config in separate repositories (or at least separate paths) is a CNOE best practice:

- **Code repo changes** trigger CI (build, test, scan)
- **Config repo changes** trigger CD (deploy, reconcile)
- Different access controls -- developers write code, automation writes config
- Config repo serves as the audit log for what was deployed and when

## CNOE Perspective

CNOE endorses Git for both code and config repositories (see [[CNOE-Technology-Choices]]). The pluggability principle means the same config repo works with either ArgoCD or Flux. The same CI pipeline output (container images, manifests) feeds any CD controller.

## See Also

- [[KRM-Format]] -- The at-rest manifest format stored in config repos
- [[CI-CD]] -- CI and CD tools that operate on these repositories
- [[Controller-Pattern]] -- Reconciliation loop connecting Git to clusters
- [[Secrets-Management]] -- Why secrets stay out of Git
- [[Infrastructure-as-Code]] -- IaC manifests also stored in config repos
- [[CNOE]] -- Framework overview
