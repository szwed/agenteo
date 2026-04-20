# Data Fabric Principles

Three principles for service resources:

1. **Self-descriptive** - resources must describe themselves
2. **Discoverable** - resources must be findable
3. **Aligned metadata** - resources must use metadata that is aligned and descriptive

These ensure interoperability and usability across services.

## O2O Example

Three systems (CRM, ERP, OMS) supporting the Opportunity-to-Order process with core business objects: Customer, Quote, Sales Order, Product.

Without metadata: integrators need domain expertise and substantial effort for correct integration.

With self-describing resources and metadata defining business object associations: it becomes evident which resources are available in each system, enabling integration configuration:
1. Replicate Customer master data between systems
2. Replicate Product master data between systems
3. Manage opportunities and generate Quotes
4. Create Sales Orders referencing Quotes

See also: [[Data-Fabric]], [[Data-Fabric-Components]]
