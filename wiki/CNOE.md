# CNOE (Cloud Native Operational Excellence)

_Pronounced "Kuh-noo"_

CNOE is a framework that brings together enterprises operating at scale to navigate operational technology decisions collectively, de-risk tooling bets, coordinate contributions, and offer guidance on which CNCF technologies to use together for cloud efficiency.

In the ApeiroRA context, CNOE provides the community-validated technology choices that inform the [Platform Mesh](8-platform-mesh/Platform-Mesh.md) tooling layer and the broader [Apeiro Reference Architecture](Apeiro-Reference-Architecture.md).

## Problem Statement

Infrastructure and tooling fragmentation has five root causes:

1. **Moving-target standards** -- The CNCF landscape is vast; organizations face paralysis of choice, adopting tools in environment-specific ways with no consensus. This creates supportability and maintainability problems.
2. **Blurred CI/CD boundaries** -- Legacy CI/CD systems are bloated. Lighter tools (ArgoCD, Flux, Tekton) focus on GitOps paradigms, but the line between CI and CD is unclear.
3. **Declarative control-plane shift** -- Kubernetes creates an ecosystem fundamentally different from previous-generation tooling, yet many workloads still require VM or bare-metal interfaces.
4. **Developer/delivery disconnect** -- Developer workflows focus on language and framework, while `*-Ops` abstractions address infrastructure differences, creating a gap between development and delivery.
5. **Packaging fragmentation** -- Multiple languages, IaC platforms, templating engines, specs, and packaging systems produce non-portable software components.

## Six Tenets

1. **Open source first** -- Prioritize OSS over proprietary technology in every vertical. Enables coordination and freedom to modify.
2. **Community driven** -- Technology selection, commitment level, and contribution direction are driven by the community and its governing body.
3. **Tools, not practices** -- CNOE suggests tools and configurations. What practices a company builds around them is out of scope.
4. **Powered by Kubernetes** -- Kubernetes is the de-facto operating environment for CNOE tooling. However, workloads can orchestrate against any compute platform (ECS, Cloud Functions, VMs). See [Control Data Work Planes](4-kubernetes/Control-Data-Work-Planes.md).
5. **Standardized infrastructure, customizable by developers** -- Platform requirements are enforced by security engineers and infra operators; usability is guaranteed by platform operators and app developers.
6. **Built to be shared** -- All deliverables (reference architecture, deployment packages) are developed in the open, collaboratively, for the broader OSS community.

## What CNOE Is NOT

- Not only a unified control plane -- it provides building blocks to extend one.
- Not only CI/CD -- it includes capabilities that extend integration and delivery.
- Not new technologies or managed services -- it is a way to integrate existing tools. Organizations still fund and operate the OSS tools.
- Not installers or proprietary packaging -- fully open source, customizable, available to anyone.
- Not responsible for operationalizing the toolchain -- organizations own operations.

## Personas

| Persona | Focus |
|---------|-------|
| **Application Developers** | Business-logic code, programming languages and frameworks, minimal interest in infra beyond what their apps use. |
| **Package Builders** | Stitch components into reusable blueprints; wrap infra and app parts into deployable units for developers. |
| **Infrastructure Operators** | Deploy and manage infra and platform components. IaC, networking, storage, orchestration. |
| **Information Security Engineers (ISE)** | Enforce security and compliance; partner with package builders to approve production-ready packages. |

## Approach

- **Pluggability and extensibility** -- Split DevOps into subcategories with logical boundaries. Any endorsed tool from one category integrates with endorsed tools from another (e.g., Tekton or Argo Workflows for CI combined with Flux or ArgoCD for CD). See [CI CD](4-kubernetes/CI-CD.md).
- **Kubernetes-powered** -- CNCF tools run on Kubernetes but can orchestrate against any target. See [KRM](4-kubernetes/KRM.md).
- **Building patterns and tooling** -- Packaging specs, templating mechanisms, and deployer technologies (e.g., [IDPBuilder](10-portals/IDP-Reference-Implementation.md)) enable bundling and sharing of recommended tool stacks.

## Key Pages

- [CNOE Technology Choices](CNOE-Technology-Choices.md) -- Capability-to-technology mapping
- [IDP Reference Implementation](10-portals/IDP-Reference-Implementation.md) -- CNOE reference IDP (IDPBuilder)
- [CI CD](4-kubernetes/CI-CD.md) -- Continuous integration and delivery
- [Infrastructure as Code](4-kubernetes/Infrastructure-as-Code.md) -- IaC approaches (Terraform, Crossplane)
- [Developer Portal](10-portals/Developer-Portal.md) -- Software catalog and developer experience
- [GitOps and Repositories](4-kubernetes/GitOps-and-Repositories.md) -- Code repos, config repos, GitOps pattern
- [Validation and Policy](4-kubernetes/Validation-and-Policy.md) -- Admission control and policy
- [Service Discovery](4-kubernetes/Service-Discovery.md) -- Dynamic service lookup
- [Signing and Supply Chain](4-kubernetes/Signing-and-Supply-Chain.md) -- Supply chain security
