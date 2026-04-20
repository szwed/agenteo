# Security Compliance Automation

## Scope

Focused on ISMS (Information Security Management System) based on single or multi control frameworks and their certifications. Supports ISO 27001, NIST SP 800-53, and others.

## Secure Controls Framework (SCF)

Uses [SCF](https://securecontrolsframework.com/) as reference. Includes ISO 27001 v2022 and NIST SP 800-53 rev5 mapped to many other frameworks.

**UIDs** - unique control IDs (framework ID + control ID) enable automation. Mandatory for mapping, traceability, and interoperability.

## Correlation IDs

OCM component version identifiers serve as correlation IDs for end-to-end request tracing, debugging, audit trails, and compliance across distributed systems.

## Architecture Principles

1. Open, standard **security controls framework** with UIDs ready for automation (SCF)
2. Open **model** with unique correlation IDs ready for automation (OCM)

## Value Proposition

Transition from **tool-centric** to **model-centric** setup:
- OCM-based IDs correlate audit-relevant facts across the development and qualification process
- More tools adopting OCM Coordinates = more content correlated end-to-end
- **OCM Gear** - extensible toolbox as OCM reference implementation; central process engine correlating metadata using OCM identities; integrates with scanners and external data sources
- Audit-safe re-prioritization reduces false positive fatigue

See also: [Software Bill of Delivery](../5-software-delivery/Software-Bill-of-Delivery.md), [Security](Security.md)
