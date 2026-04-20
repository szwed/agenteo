# CI/CD (Continuous Integration / Continuous Delivery)

CI/CD in cloud-native environments has evolved beyond monolithic tools like Jenkins and Spinnaker. CNOE distinguishes CI and CD as separate capability categories with distinct tool choices, while ApeiroRA frames them within the [[Controller-Pattern]] and [[KRM]] reconciliation model.

## Continuous Delivery (CD)

CD focuses on getting validated artifacts deployed to target environments. In Kubernetes-native platforms, CD is implemented through **reconciling controllers** that continuously sync desired state from Git to clusters.

**Key tools:**
- **ArgoCD** -- Declarative GitOps CD for Kubernetes. Monitors Git repositories and reconciles cluster state to match. Uses the [[Controller-Pattern]] (watch, diff, act).
- **FluxCD** -- Alternative GitOps toolkit. Also a reconciling controller, with a more composable architecture (source controller, kustomize controller, helm controller).

Both operate as Kubernetes controllers -- they do not "push" deployments but continuously reconcile desired vs actual state. This is the same pattern that drives [[Digital-Twins]] and [[KRM-Control]].

## Continuous Integration (CI)

CI covers build, test, and validation workflows that run before artifacts reach CD.

**Key tools:**
- **Argo Workflows** -- Kubernetes-native workflow engine. DAG and step-based pipelines defined as CRDs. Scalable for large workloads (CNOE has published scalability benchmarks).
- **Tekton** -- Kubernetes-native CI/CD pipeline framework. Tasks and pipelines as CRDs. Strong separation of concerns between task definition and pipeline orchestration.

Both are Kubernetes-native, meaning pipeline definitions are [[KRM-Format]] resources managed through the API server.

## CD vs CI: The Distinction

| Aspect | CI | CD |
|--------|----|----|
| Trigger | Code push, PR | CI completion, Git commit to config repo |
| Model | Run-to-completion workflows | Continuous reconciliation loop |
| Tools | Argo Workflows, Tekton | ArgoCD, FluxCD |
| Output | Tested artifacts, images, manifests | Deployed workloads |

CNOE treats these as separate pluggable categories. Any CI tool works with any CD tool -- Tekton pipelines can produce manifests that ArgoCD deploys, or Argo Workflows can build images that Flux rolls out.

## Deployment Strategies

- **Blue/Green** -- Two identical environments; traffic switches after validation. ArgoCD supports this via Argo Rollouts.
- **Canary** -- Gradual traffic shift to new version. Argo Rollouts provides automated canary analysis.
- **Feature flags** -- Decouple deployment from release. Orthogonal to CD tooling but integrates at the application layer.

## CNOE Perspective on Pluggability

CNOE defines logical boundaries between CI and CD so organizations can mix tools:

> Assuming users choose between Tekton or Argo Workflows for CI and Flux or ArgoCD for CD, any combination should work within CNOE.

This reduces fragmentation while providing options. The [[CNOE-Technology-Choices]] page maps these selections.

## See Also

- [[Controller-Pattern]] -- Reconciliation model underlying GitOps CD
- [[GitOps-and-Repositories]] -- Code and config repositories that feed CI/CD
- [[Infrastructure-as-Code]] -- IaC resources also delivered through CD pipelines
- [[IDP-Reference-Implementation]] -- CNOE reference stack includes ArgoCD and Argo Workflows
- [[CNOE]] -- Framework overview
