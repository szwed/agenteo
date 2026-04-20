# LCM Operator-based Installation

Operator-based LCM implements installation and upgrade procedures with application-specific code rather than general-purpose tools. The operator coordinates steps for installing/updating an application, considering configuration and current environment state.

In Kubernetes: operator = custom controller, configuration = custom resource, reconciliation loop ensures desired state.

## Four Principles

1. **API First** - design rich, versioned APIs for holistic management; avoid unstructured data
2. **Declarative API** - use desired states; remodel imperative APIs; embrace async responses
3. **Reconciling controllers** - continuously monitor and align desired vs observed state; embed migration/upgrade logic in the controller
4. **Data and Metadata in Data Plane** - all configuration data queryable via API with consistent model; enables emergent functionality

These principles allow the controller implementation behind a versioned API contract to be exchanged without breaking changes.

See also: [Lifecycle Management](Lifecycle-Management.md)
