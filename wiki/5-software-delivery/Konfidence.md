# Konfidence

Software delivery framework for microservice-based SaaS applications.

## Core Features

- **Immutable application vectors** - versioned, complete deployment definitions
- **Stage-based delivery flows** - promotion across DEV, TEST, PROD after validation
- **Feature control** - feature toggles and ring deployments for progressive rollouts
- **Automated governance** - vector usage tracking, automatic cleanup of outdated deployments

## Delivery Workflow

1. **Artifact build and registration** - CI produces build outputs, registers Konfidence artifact with metadata
2. **Vector creation** - assembles artifacts into immutable vector (single source of truth)
3. **Deployment to environment** - vector deployed to target environment
4. **Promotion through stages** - same vector promoted without modification after validation
5. **Lifecycle management** - tracks active vectors, removes unused ones

Shared service deployments across stages within the same landscape reduce infrastructure costs.

See also: [Konfidence Core Concepts](Konfidence-Core-Concepts.md), [Lifecycle Management](Lifecycle-Management.md)

Website: [konfidence.cloud](https://konfidence.cloud)
