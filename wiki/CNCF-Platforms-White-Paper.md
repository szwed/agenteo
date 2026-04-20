# CNCF Platforms White Paper

Source: [CNCF TAG App Delivery — Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)

## What Is an Internal Platform?

An integrated collection of capabilities defined and presented according to the needs of the platform's users. It is a cross-cutting layer ensuring consistent experience for acquiring and integrating typical capabilities and services across applications and use cases.

> "A digital platform is a foundation of self-service APIs, tools, services, knowledge and support which are arranged as a compelling internal product." — Martin Fowler & Evan Bottcher

Platforms bridge between **capability providers** (cloud services, infra teams) and **platform users** (app developers, data scientists, operators). Platform teams own the interfaces and user experience, not necessarily the backing implementations.

## Why Platforms?

1. **Reduce cognitive load** on product teams — accelerate development and delivery
2. **Improve reliability** by dedicating experts to configure and manage shared capabilities
3. **Accelerate reuse** of tools and knowledge across the enterprise
4. **Reduce risk** of security, regulatory, and functional issues through governed capabilities
5. **Cost-effective cloud use** by delegating to managed providers while controlling UX

## Attributes of Successful Platforms

| Attribute | Description |
|---|---|
| **Platform as a product** | Designed and evolved based on user requirements, not top-down mandates |
| **User experience** | Consistent interfaces: GUIs, APIs, CLIs, IDEs, portals |
| **Documentation & onboarding** | Golden paths, templates, examples |
| **Self-service** | On-demand provisioning with minimal manual intervention |
| **Reduced cognitive load** | Encapsulate implementation details, hide complexity |
| **Optional & composable** | Teams use only parts they need; can bring their own capabilities |
| **Secure by default** | Built-in compliance, validation, policy enforcement |

## Platform Capabilities

The whitepaper identifies 13 capability domains:

- Web portals (Backstage, Skooner)
- APIs and CLIs (Kubernetes, Crossplane, Helm)
- Golden path templates and docs
- Build and test automation (Tekton, Jenkins)
- Delivery and verification (Argo, Flux, Keptn)
- Development environments (Devfile, Telepresence)
- Observability (OpenTelemetry, Prometheus, Grafana)
- Infrastructure services (Kubernetes, Knative, CNI)
- Data services (TiKV, Vitess)
- Messaging and events (NATS, Strimzi, Dapr)
- Identity and secrets (SPIFFE/SPIRE, cert-manager, Keycloak)
- Security (Falco, OPA, Kyverno)
- Artifact storage (Harbor, OCI Distribution)

## Challenges

- Platforms must be treated as **products**, developed with users, not imposed on them
- Choose initial capabilities and partner teams carefully
- Gain **leadership support** by demonstrating direct impact on value streams
- Build the **thinnest viable platform** layer over managed providers

## Platform Teams

Responsibilities:
1. Research user requirements, plan roadmap
2. Market, evangelize, and advocate the platform
3. Develop interfaces (portals, APIs, docs, templates, CLIs)

Platform teams do not necessarily run infrastructure. They own the **experience layer** and rely on capability providers for backing implementations.

## Measuring Success

- **User satisfaction**: NPS, active users, retention, SPACE framework
- **Organizational efficiency**: request-to-fulfillment latency, time to first deploy
- **Product delivery**: DORA metrics (deployment frequency, lead time, MTTR, change failure rate)

## Mapping to ApeiroRA

ApeiroRA's [[Platform-Mesh]] directly implements the CNCF platform vision:

- [[Service-Concepts]] and [[Managed-Service-Provider-Pattern]] provide the capability provider abstraction
- [[User-Facing-Control-Plane]] (kcp) and [[Service-Provider-Control-Planes]] deliver the self-service API layer
- [[Developer-Portal]] (Backstage) covers the web portal capability
- [[Observability]] (OpenTelemetry) maps to the observability domain
- [[Security]] with [[Validation-and-Policy]] and [[Security-Compliance-Automation]] address secure-by-default

See also: [[Platform-Maturity-Model]] for assessing your platform engineering journey.
