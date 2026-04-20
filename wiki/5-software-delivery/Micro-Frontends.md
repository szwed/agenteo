# Micro Frontends

Architectural pattern for integrating independently developed UIs of microservice components into a consistent holistic interface. Apeiro adopts [[OpenMFP]] as the key integration component.

## Challenges

- Redundant implementations (auth, permissions duplicated across teams)
- Integration difficulties (isolated services hard to combine)
- Fragmented user experience (multiple interfaces)

## Key Characteristics

- **Independence** - self-contained with own codebase, dependencies, lifecycle
- **Technology Agnostic** - teams choose their own stacks
- **Autonomous** - teams work independently, faster iterations
- **Loose Coupling** - changes in one part don't impact others

## Implementation Approaches

- **Server-side** - server composes micro frontends before sending to client
- **Build-time** - combined during build process
- **Runtime** (preferred) - central container loads micro frontends dynamically

## Composition

- **Full Page Integration** - load complete page/route from single micro frontend via iframe; simpler
- **Page Composition via Web Components** - compose pages from multiple micro frontends in defined slots; more flexible

## Common UX Guidelines

Design system, consistent navigation, unified auth, communication API, compatibility/localization/accessibility.
