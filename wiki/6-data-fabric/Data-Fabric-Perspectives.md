# Data Fabric Perspectives

## Developer Perspective

Focuses on exposing and leveraging metadata and APIs for building and extending applications efficiently.

Data Fabric provides a suite of developer tools to minimize effort and streamline implementation:

- **ORD Plugin** - generates ORD documents for CAP or Java applications; adds a single entry point for machine-readable metadata discovery (static catalog or runtime inspection)
- **API Metadata Validator** - ensures compliance and correctness of API documentation (OpenAPI, AsyncAPI, GraphQL, ORD)
- **ORD Crawler** - retrieves and verifies metadata from ORD endpoints
- **ORD Provider Server** - exposes static metadata via HTTP using the ORD protocol without altering service runtime behavior; metadata is consumed by aggregators like the Unified Metadata Service (see [[Data-Fabric-Components]])

## Integrator Perspective

Utilizes standardized metadata and service definitions to streamline cross-system integration and ensure data consistency.

Deep understanding of system capabilities and exposed resources is essential for enabling interoperability, orchestrating workflows, mapping/transforming data, and managing APIs and event-driven communication.

- **Landscape Resource Viewer** renders a metadata graph of services and resources based on information aggregated by the Unified Metadata Service (see [[Data-Fabric-Components]])
- Visualizing relationships between resources at the business object level accelerates integration tasks and reduces implementation complexity

## Analyst Perspective

Gains access to enriched, discoverable, and well-documented data assets for faster and more accurate analysis.

Consistency of aggregated data and clear understanding of sources are key prerequisites for effective analytics.

- **Landscape Resource Viewer** provides a comprehensive view of metadata relationships (same tool as integrators, different use case)
- Visualized metadata graph reveals interconnections between service-provided resources, deployment context, and associated business objects
- Enables root-cause analysis, data lineage tracing, and improved trust in analytics output

## Service Supplier Perspective

Publishes services with aligned metadata, ensuring discoverability, traceability, and easy consumption by others.

A service supplier must register a service provider (which manages one or more services) in a service marketplace. Registration should include all necessary information for consumers, including API definitions.

- Open Resource Discovery (ORD, see [[Data-Fabric-Components]]) facilitates consistent interface modeling across distributed systems
- Enables standardized service description, discoverability, and streamlined integration within complex architectures

See also: [[Data-Fabric]], [[Data-Fabric-Components]], [[Data-Fabric-Principles]]
