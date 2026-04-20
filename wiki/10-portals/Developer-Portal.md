# Developer Portal

A developer portal is the primary interface through which application developers interact with the platform. It aggregates software catalog, API documentation, templates, and onboarding automation into a single pane. CNOE identifies developer portals as a core IDP capability; ApeiroRA addresses the same need through [[OpenMFP]] and the [[Micro-Frontends]] architecture.

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

CNOE endorses [Backstage](https://backstage.io) (see [[CNOE-Technology-Choices]]) as the developer portal technology. Key characteristics:

- **Plugin architecture** -- Extensible through frontend and backend plugins. Organizations add capabilities (Kubernetes, ArgoCD, Argo Workflows, Spark, etc.) as plugins.
- **Software catalog** -- Entity model with Components, APIs, Resources, Systems, and Groups.
- **Software templates** -- YAML-defined scaffolding actions (create repo, register component, deploy via ArgoCD).
- **TechDocs** -- Docs-as-code, rendered from Markdown in source repos.

In the [[IDP-Reference-Implementation]], Backstage is configured with Keycloak SSO, ArgoCD integration, and Argo Workflows visibility. Developers create deployments, Spark jobs, and cloud resources through Backstage templates.

## Relation to OpenMFP and ApeiroRA

Where CNOE uses Backstage as a standalone portal, ApeiroRA's approach uses [[OpenMFP]] as the micro-frontend platform. OpenMFP can host Backstage-like functionality (catalog, templates) as individual micro-frontends alongside other platform UIs ([[Micro-Frontends]]).

Key differences:
- **Backstage** -- Monolithic plugin model; single React app with plugin slots.
- **OpenMFP** -- Micro-frontend composition; independent UIs from different teams composed at runtime.

Both serve the same goal: reduce cognitive load for developers by providing a unified entry point to the platform.

## CNOE Perspective

CNOE treats the developer portal as the usability layer that makes infrastructure standardization ([[Infrastructure-as-Code]]), GitOps ([[CI-CD]]), and policy ([[Validation-and-Policy]]) accessible to application developers without requiring them to understand the underlying Kubernetes machinery.

## See Also

- [[OpenMFP]] -- ApeiroRA's micro-frontend platform
- [[Micro-Frontends]] -- Composition model for platform UIs
- [[IDP-Reference-Implementation]] -- Backstage in the CNOE reference stack
- [[CNOE-Technology-Choices]] -- Technology mapping
- [[Platform-Mesh]] -- Developer portal sits in the platform mesh layer
- [[Backstage]] -- full Backstage documentation
- [[OpenMFP-Portal]] -- full OpenMFP documentation
- [[Portals-Overview]] -- comparison of portal approaches
