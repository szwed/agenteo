# Managed Service Provider Pattern

## Problem

- **Locality** - capabilities must operate in designated locations (latency, bandwidth, legal requirements)
- **Scalability** - single service runtime has limited capacity; no fundamental runtime spans across regions
- Solution requires managing **multiple service runtimes** with capability deployment close to the consumer

## Solution: Service Coordinator + Servicelet

### Service Coordinator

Central component comprising:

**Service Scheduler** - identifies and assigns appropriate service runtimes for unscheduled capabilities based on constraints (load, capacity, location, topology). Updates the resource document with runtime assignment.

**Service Runtime Manager** - manages lifecycle of service runtimes. Orders additional runtimes when scheduler cannot find suitable ones; removes runtimes no longer needed. Leverages other service providers for the runtime infrastructure.

### Servicelet

Operates on or near the service runtime(s) it manages. Monitors the service orchestration environment for resources needing deployment on its runtimes. Executes installation, reports capability status, relays runtime status as a digital twin.

**Key insight**: reverses the direction of requests (servicelet pulls from orchestration env, not pushed to). Enables fenced and hybrid environments without special network setup. Shifts operational logic to controllers at the edge.

Inspired by the **sharded controller pattern** in Kubernetes.

See also: [Service Concepts](Service-Concepts.md), [Platform Mesh Design Decisions](Platform-Mesh-Design-Decisions.md)
