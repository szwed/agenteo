# Control, Data, and Work Planes

## Control Plane

The brain: orchestrates and manages the target environment. Handles provisioning (deployment, scaling, lifecycle), configuration management (consistency, compliance), observability (monitoring, logging, alerting), and accounts/roles (access permissions).

## Data Plane

The persistency layer hosting the **shared repository** for all [[Digital-Twins|digital twin]] resources. Not to be confused with the networking data/forwarding plane.

## Work Plane

The operational heart: computational bulk work of processing, storing, and transmitting data. Can be specialized (object storage, database service) or generic (infrastructure, container runtimes).

Think of work plane as factory floor worktable; management plane as the office in another building.

## Recursive Design

Planes materialize as microservice components on runtimes. Suitable building blocks enable recursive patterns -- e.g., [[Hosted-Control-Planes]] or [[Multi-Cloud-Service-Provider]].

## CNOE Perspective

CNOE treats the **compute platform** as a deployment target with SOA-like discoverability -- services are registered and discoverable regardless of where they run. Kubernetes serves dual roles: as the compute substrate for platform capabilities (control plane tooling, CD, observability) and as one of several deployment targets. CNOE explicitly supports orchestration beyond K8s, including AWS Lambda, VMs, ECS, and static content hosting. This "powered by Kubernetes, but not limited to Kubernetes" tenet aligns with Apeiro's recursive plane model, where work planes can be specialized or generic compute.

See also: [[Kubernetes-Implementation-Design]], [[Controller-Archetypes]], [[Multi-Plane-Controller]]
