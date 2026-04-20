# Portals Overview

Developer portals and micro frontend platforms provide a unified UI layer for cloud-native platforms, replacing fragmented tool-specific interfaces with a single entry point for developers and operators.

## Two Approaches

### Backstage

CNCF Graduated project, created by Spotify. An open framework for building developer portals centered on a **software catalog**.

- Unified registry of all software entities (services, libraries, APIs, resources)
- Software Templates for scaffolding new projects with baked-in best practices
- TechDocs for docs-as-code
- Plugin ecosystem (200+ open-source plugins)
- Focus: **developer productivity** -- catalog, templates, documentation, search

See [Backstage](Backstage.md) for full details.

### OpenMFP

Open Micro Frontend Platform from ApeiroRA / NeoNephos Foundation. A **micro frontend composition runtime** with Kubernetes-native lifecycle management.

- Runtime integration of independent micro frontends via Luigi framework
- ContentConfiguration CRD for declarative UI extension management
- Technology-agnostic -- teams choose their own frontend stack
- Focus: **runtime UI composition** -- independent release cycles, multi-team autonomy

See [OpenMFP Portal](OpenMFP-Portal.md) for full details.

## Comparison

| Aspect               | Backstage                        | OpenMFP                                 |
| -------------------- | -------------------------------- | --------------------------------------- |
| Model                | Developer portal framework       | Micro frontend runtime platform         |
| Integration          | Plugin system (single React app) | Runtime micro frontend composition      |
| Catalog              | Core feature (catalog-info.yaml) | Not primary focus                       |
| K8s-native lifecycle | No (Node.js app)                 | Yes (ContentConfiguration CRD)          |
| CNCF status          | Graduated                        | Not CNCF (NeoNephos / Linux Foundation) |

Both aim to solve UI fragmentation. Backstage centralizes developer tooling around a catalog. OpenMFP composes independent UIs from multiple teams at runtime.

## See Also

- [Developer Portal](Developer-Portal.md) -- developer portal as an IDP capability
- [Micro Frontends](../5-software-delivery/Micro-Frontends.md) -- micro frontend architecture in ApeiroRA
