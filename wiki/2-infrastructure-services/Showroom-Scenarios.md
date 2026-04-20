# Showroom Scenarios

A "Showroom" is a functioning deployment of Apeiro components -- useful for integration testing, demos, or as a production starting point.

> **Status:** Early stage. Scenarios will evolve as components mature.

## Application and Service Platform

Build on existing IaaS; infrastructure layer replaceable with Apeiro components later.

### Application Hosting

Core: Gardener + Platform Mesh + OpenMFP + OpenFGA
External: OCI repository, IdP, logging/monitoring stack
Requires: Gardener-supported infra provider

Install docs: [Gardener](https://gardener.cloud/docs/gardener/deployment/setup_gardener/) | [OpenMFP](https://openmfp.org/documentation/getting-started/installation) | [OpenFGA](https://openfga.dev/docs/getting-started/setup-openfga/overview) | [kcp](https://docs.kcp.io/kcp/main/setup/)

### Lifecycle and Installation

Adds: OCM + OpenMCP on top of Application Hosting
External: OCI registry
Install: [OCM](https://ocm.software/docs/getting-started/installation/)

### Development and Management

Adds: Data Fabric capabilities on top of other scenarios.

## Infrastructure and Baremetal

Full cloud stack from hardware to services. Requires [hardware investment](../1-bare-metal/Hardware-Recommendations.md) and BOS layer setup.

### Baremetal Automation

Set up racks per [hardware specs](../1-bare-metal/Hardware-Control-Plane.md). Low-level hardware coupling may require code adjustments for your specific hardware.

### Infrastructure as a Service

Add IronCore or CobaltCore on top of baremetal automation. Enables Gardener and all Application Platform scenarios above.
