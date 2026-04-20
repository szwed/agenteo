# Data Fabric Landscape

Metadata flow through the system landscape:

## 1. Self-Description via ORD

- All exposed resources (APIs, Events) provide metadata definitions including primary and referenced business objects
- Each service exposes ORD documents through a well-known configuration endpoint

## 2. Aggregation via UMS

UMS serves as central ORD aggregator. Retrieves metadata from services, stores it in the metadata repository per the onboarded metadata model, and exposes it via discovery components.

Prerequisite: metadata model must be onboarded into UMS.

## 3. Visualization and Consumption

Landscape resource viewer acts as ORD consumer, providing visual representation of aggregated metadata as a metadata graph. Additional consumption use cases supported.

See also: [Data Fabric Components](Data-Fabric-Components.md), [Data Fabric](Data-Fabric.md)
