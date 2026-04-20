# Backstage

[Backstage](https://backstage.io/) is a CNCF Graduated open-source framework for building developer portals, created by Spotify. It provides a centralized software catalog that restores order to microservices and infrastructure, enabling product teams to ship high-quality code without compromising autonomy.

## Core Features

### Software Catalog

A centralized registry of all software in the ecosystem -- services, websites, libraries, data pipelines, ML models. Entities are described via `catalog-info.yaml` files stored in source control alongside the code.

Key capabilities:
- Ownership and metadata tracking for all software
- Entity model: Components, APIs, Resources, Systems, Groups
- Auto-discovery from Git providers (GitHub, GitLab, Bitbucket, Azure DevOps)
- Integrated tooling via plugins attached to catalog entities

### Software Templates (Scaffolder)

A tool for creating new projects from templates with organizational best practices baked in. Templates are YAML-defined and can:
- Load code skeletons and template variables
- Create Git repositories
- Register new components in the catalog
- Trigger CI/CD pipelines and ArgoCD deployments

### TechDocs

Docs-like-code solution built into Backstage. Engineers write Markdown in their source repos; Backstage auto-generates and serves documentation sites. Built on MkDocs with support for the MkDocs plugin ecosystem.

- 5000+ documentation sites at Spotify
- Supports GitHub, GitLab, Bitbucket, Azure DevOps, Gerrit, Gitea
- Storage: local filesystem, GCS, S3, Azure Blob Storage

### Kubernetes Integration

Service-owner-oriented view of Kubernetes resources. Developers check the health of their services across clusters -- local, staging, and production -- without needing cluster admin access. Surfaces deployments, pods, and errors for catalog entities.

### Search

Unified search across the catalog, TechDocs, APIs, and any plugin-provided content. Pluggable search engine backends.

### AI Skills

Backstage publishes curated AI skills -- self-contained guidance files that teach AI coding assistants how to perform common Backstage engineering tasks. Skills are installed via `npx skills add https://backstage.io` and follow a SKILL.md convention.

## Architecture

Three main components:

- **Frontend** -- React-based SPA with an extension system. Plugins register as extensions attached to a tree structure. Routing system provides indirection so plugins can link to each other without hardcoded paths.
- **Backend** -- Node.js service(s). Each backend plugin is an independent microservice that communicates over the wire. Can be deployed as a single backend or split into multiple deployment units.
- **Database** -- PostgreSQL (production) or SQLite (development). Each plugin gets a logically separated database via Knex.

Plugin architecture supports three patterns:
1. **Standalone** -- frontend-only, no API calls (e.g., Tech Radar)
2. **Service backend** -- calls an organization-hosted service (e.g., Lighthouse)
3. **Third-party backend** -- calls external SaaS APIs through a proxy (e.g., CircleCI)

## Plugin Ecosystem

200+ open-source plugins covering Kubernetes, ArgoCD, Argo Workflows, PagerDuty, Datadog, Grafana, Jenkins, GitHub Actions, and many more. Organizations also build internal plugins for company-specific tooling.

## CNOE Reference

Backstage is the endorsed developer portal in the CNOE framework (see [CNOE Technology Choices](../CNOE-Technology-Choices.md)). In the [IDP Reference Implementation](IDP-Reference-Implementation.md), Backstage is configured with:
- Keycloak SSO
- ArgoCD integration
- Argo Workflows visibility
- Templates for creating deployments, Spark jobs, and cloud resources

Backstage is also the "B" in the [BACK Stack](../BACK-Stack.md) (Backstage + ArgoCD + Crossplane + Kyverno).

## Comparison with OpenMFP

| Aspect | Backstage | OpenMFP |
|---|---|---|
| Approach | Catalog-centric developer portal | Composition-centric micro frontend runtime |
| Extension model | Plugins within a single React app | Independent micro frontends composed at runtime |
| Target user | Developers (catalog, templates, docs) | Platform operators (UI composition, multi-team) |
| K8s lifecycle | Views K8s resources | Manages UI extensions as K8s CRDs |

See [OpenMFP Portal](OpenMFP-Portal.md) for full OpenMFP documentation.

## Links

- https://backstage.io
- https://github.com/backstage/backstage
- [Portals Overview](Portals-Overview.md) -- comparison of portal approaches
- [Developer Portal](Developer-Portal.md) -- developer portal as an IDP capability
