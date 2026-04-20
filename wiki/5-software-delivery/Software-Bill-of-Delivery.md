# Software Bill of Delivery

The Open Component Model (OCM) serves as the Software Bill of Delivery (SBoD), going beyond SBoM to facilitate integrity, security, and traceability holistically.

## Key Features

- **Machine-readable** - technology-agnostic, open standard for describing software artifacts
- **Integrity and Provenance** - signed components, verifiable chain of custody, routing-slips
- **Secure Transport** - content transported to any environment (public cloud, on-premise, air-gapped)
- **Correlation ID** - unique component identifier enables traceability across the software lifecycle
- **Automated Deployment** - GitOps techniques, declarative APIs, reproducible Infrastructure as Data deployments

## Release Channel

OCM serves as a release channel containing the qualified version vector of all subcomponents. Consumers subscribe to a release repository to discover published versions and receive notifications of new versions.

## Security Compliance

The OCM coordinate system is the crucial link for [Security Compliance Automation](../8-platform-mesh/Security-Compliance-Automation.md). It provides unique component version identifiers that correlate SBoMs and scanner signals in a backoffice data lake.

## CNOE Perspective

CNOE uses **OCI-compliant container registries** as artifact registries, emphasizing signed and traceable artifacts with software supply-chain security (SSSC) best practices. For packaging and templating, CNOE supports multiple distribution mechanisms (OCI artifacts, Helm, Kustomize) deployed via GitOps (Argo CD, Flux). This aligns with Apeiro's OCM-based SBoD approach -- both treat OCI registries as the transport layer for signed components. Where Apeiro uses OCM as the unifying abstraction for machine-readable bills of delivery, CNOE provides the complementary CI/CD pipeline and registry infrastructure that produces and consumes those artifacts.

See also: [Lifecycle Management](Lifecycle-Management.md)
