# Platform Mesh Perspectives

## Developer Perspective

1. **Identify target environment** - available services vary (public cloud vs air-gapped vs edge)
2. **Create account** - credentials and permissions from external system
3. **Find services** - browse service marketplaces, select from multiple providers
4. **Order capabilities** - create KRM resource documents describing desired state; service provider detects changes and implements them (digital twin pattern)
5. **Run application** - deployment depends on chosen runtime; tools available for air-gapped/edge scenarios

Managed services use the full provider lifecycle; unmanaged services are deployed outside Apeiro.

## Service Supplier Perspective

1. **Service lifecycle API** - capability lifecycle controllable via declarative model (KRM); lifecycle API and business API must be decoupled
2. **Register in marketplace** - provide service description, API definitions, SLAs, technical details; marketplace controller provisions connection info
3. **Provide services** - controller monitors for resource document changes and reconciles them

## Operator Perspective

1. **Set up service orchestration environment** - Apeiro provides toolbox, not turnkey; requires integration with IdP, contracts/CRM, billing
2. **Maintain marketplaces** - register service providers, align with commercial model, ongoing maintenance

See also: [[Platform-Mesh]]
