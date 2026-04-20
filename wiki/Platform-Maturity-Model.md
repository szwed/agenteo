# Platform Engineering Maturity Model

Source: [CNCF TAG App Delivery — Platform Engineering Maturity Model](https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/)

Companion to the [CNCF Platforms White Paper](CNCF-Platforms-White-Paper.md). That paper describes **why and what** to build; this model describes **how to plan and assess progress**.

## How to Use the Model

- Each aspect is evaluated **independently** — an org can be Level 3 in Interfaces but Level 1 in Measurement
- Higher levels require more investment; reaching Level 4 is not a goal in itself
- Goal: find yourself in the model, then identify opportunities in adjacent levels

## Five Aspects, Four Levels

| Aspect | Question | L1 Provisional | L2 Operational | L3 Scalable | L4 Optimizing |
|---|---|---|---|---|---|
| **Investment** | How are staff/funds allocated? | Voluntary / temporary | Dedicated team | As product | Enabled ecosystem |
| **Adoption** | Why/how do users discover and use platforms? | Erratic | Extrinsic push | Intrinsic pull | Participatory |
| **Interfaces** | How do users interact with capabilities? | Custom processes | Standard tooling | Self-service solutions | Integrated services |
| **Operations** | How are platforms planned, developed, maintained? | By request | Centrally tracked | Centrally enabled | Managed services |
| **Measurement** | How is feedback gathered and incorporated? | Ad hoc | Consistent collection | Insights | Quantitative + qualitative |

## Aspect Details

### Investment

- **L1**: Tiger teams, hack-day efforts, no dedicated funding
- **L2**: Dedicated team (DevOps/DevEx/Shared Tools), treated as cost center
- **L3**: Product management, UX roles, roadmap, chargeback system
- **L4**: Specialists (security, perf, quality) extend platform; ecosystem contributions

### Adoption

- **L1**: Ad hoc tool discovery, no org-wide strategy
- **L2**: Mandates or incentives drive use; fragmented uptake
- **L3**: Users choose platform for its clear value; self-serve portals and golden paths
- **L4**: Users contribute back (fixes, features, new capabilities)

### Interfaces

- **L1**: Custom manual processes, person-to-person knowledge
- **L2**: Paved roads / golden paths via docs and templates; still requires domain expertise
- **L3**: One-click self-service; consistent API abstractions
- **L4**: Capabilities transparently integrated into developer workflows (IDE, CI, runtime)

### Operations

- **L1**: Reactive, ad hoc; no maintenance plan; bespoke upgrades
- **L2**: Central inventory, IaC, compliance tracking
- **L3**: Central orchestration, standard lifecycle processes, CD for platform capabilities
- **L4**: Fully automated lifecycle; shared responsibility model; zero-impact upgrades

### Measurement

- **L1**: No standard metrics; anecdotal decisions
- **L2**: Intentional feedback collection (surveys, usage data); feature success measured
- **L3**: Desired outcomes defined first, then metrics chosen; industry frameworks (DORA, SPACE)
- **L4**: Data democratized; qualitative + quantitative; Goodhart's Law awareness; SLOs

## Mapping to ApeiroRA Components

| Level | ApeiroRA capabilities at this stage |
|---|---|
| L1 Provisional | Manual scripts, wiki docs, ad hoc Kubernetes clusters |
| L2 Operational | [Managed Kubernetes as a Service](3-cluster-management/Managed-Kubernetes-as-a-Service.md) (Gardener), basic [CI CD](4-kubernetes/CI-CD.md), central [Observability](8-platform-mesh/Observability.md) |
| L3 Scalable | [Platform Mesh](8-platform-mesh/Platform-Mesh.md) self-service APIs, [Developer Portal](10-portals/Developer-Portal.md), [Service Concepts](8-platform-mesh/Service-Concepts.md) catalog, [KRM](4-kubernetes/KRM.md) abstractions |
| L4 Optimizing | Full [Platform Mesh](8-platform-mesh/Platform-Mesh.md) with [Managed Service Provider Pattern](8-platform-mesh/Managed-Service-Provider-Pattern.md), [Security Compliance Automation](8-platform-mesh/Security-Compliance-Automation.md), [AI Agents Overview](9-ai-agents/AI-Agents-Overview.md) for autonomous operations |

## See Also

- [CNCF Platforms White Paper](CNCF-Platforms-White-Paper.md)
- [Platform Mesh](8-platform-mesh/Platform-Mesh.md)
- [BACK Stack](BACK-Stack.md)
