# Developer Portal

A developer portal is the primary interface through which application developers interact with the platform. It aggregates software catalog, API documentation, templates, and onboarding automation into a single pane. CNOE identifies developer portals as a core IDP capability; ApeiroRA addresses the same need through [OpenMFP](../5-software-delivery/OpenMFP.md) and the [Micro Frontends](../5-software-delivery/Micro-Frontends.md) architecture.

## Core Capabilities

### Software Catalog
A registry of all services, libraries, and infrastructure components in the organization. Each entry (entity) includes ownership, dependencies, lifecycle status, and links to source code, CI/CD, and monitoring.

### API Documentation
Auto-discovered or manually registered API specs (OpenAPI, gRPC, AsyncAPI). Developers can browse and understand available APIs without hunting through wikis or Slack.

### Software Templates
Scaffolding for new projects. Templates encode organizational standards (repo structure, CI pipeline, required metadata, security scans) so every new service starts compliant. In the CNOE reference implementation, Backstage templates create Git repos, ArgoCD applications, and catalog entries in a single flow.

### Onboarding Automation
New team members or projects get access, repositories, pipelines, and infrastructure provisioned through the portal rather than manual tickets.

## Backstage as Reference

CNOE endorses [Backstage](https://backstage.io) (see [CNOE Technology Choices](../CNOE-Technology-Choices.md)) as the developer portal technology. Key characteristics:

- **Plugin architecture** -- Extensible through frontend and backend plugins. Organizations add capabilities (Kubernetes, ArgoCD, Argo Workflows, Spark, etc.) as plugins.
- **Software catalog** -- Entity model with Components, APIs, Resources, Systems, and Groups.
- **Software templates** -- YAML-defined scaffolding actions (create repo, register component, deploy via ArgoCD).
- **TechDocs** -- Docs-as-code, rendered from Markdown in source repos.

In the [IDP Reference Implementation](IDP-Reference-Implementation.md), Backstage is configured with Keycloak SSO, ArgoCD integration, and Argo Workflows visibility. Developers create deployments, Spark jobs, and cloud resources through Backstage templates.

## Relation to OpenMFP and ApeiroRA

Where CNOE uses Backstage as a standalone portal, ApeiroRA's approach uses [OpenMFP](../5-software-delivery/OpenMFP.md) as the micro-frontend platform. OpenMFP can host Backstage-like functionality (catalog, templates) as individual micro-frontends alongside other platform UIs ([Micro Frontends](../5-software-delivery/Micro-Frontends.md)).

Key differences:
- **Backstage** -- Monolithic plugin model; single React app with plugin slots.
- **OpenMFP** -- Micro-frontend composition; independent UIs from different teams composed at runtime.

Both serve the same goal: reduce cognitive load for developers by providing a unified entry point to the platform.

## CNOE Perspective

CNOE treats the developer portal as the usability layer that makes infrastructure standardization ([Infrastructure as Code](../4-kubernetes/Infrastructure-as-Code.md)), GitOps ([CI CD](../4-kubernetes/CI-CD.md)), and policy ([Validation and Policy](../4-kubernetes/Validation-and-Policy.md)) accessible to application developers without requiring them to understand the underlying Kubernetes machinery.

## See Also

- [OpenMFP](../5-software-delivery/OpenMFP.md) -- ApeiroRA's micro-frontend platform
- [Micro Frontends](../5-software-delivery/Micro-Frontends.md) -- Composition model for platform UIs
- [IDP Reference Implementation](IDP-Reference-Implementation.md) -- Backstage in the CNOE reference stack
- [CNOE Technology Choices](../CNOE-Technology-Choices.md) -- Technology mapping
- [Platform Mesh](../8-platform-mesh/Platform-Mesh.md) -- Developer portal sits in the platform mesh layer
- [Backstage](Backstage.md) -- full Backstage documentation
- [OpenMFP Portal](OpenMFP-Portal.md) -- full OpenMFP documentation
- [Portals Overview](Portals-Overview.md) -- comparison of portal approaches
