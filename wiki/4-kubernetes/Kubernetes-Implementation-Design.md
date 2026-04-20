# Kubernetes Implementation Design

Kubernetes is composed of microservices forming three planes. Key distinction: unlike typical microservices with own state/API, Kubernetes defines a common API framework and manages state for all components in the [data plane](Control-Data-Work-Planes.md).

## Data Plane

- **etcd** (or SQLite/RDBMS in K3s) for persistence
- **API server** -- generic, no use-case-specific opinion (cf. kcp generic control plane)
- Provides controlled access to shared repository of [digital twin](Digital-Twins.md) resources

## Control Plane

- API extensions (CRDs, Extension API Servers)
- **Scheduler** -- assigns pods to nodes
- **Controller manager** -- bundles internal controllers
- **Cloud controller manager** -- controllers for external cloud provider resources
- Optional features: VPA, API Gateways, etc.
- Node-level controllers (conceptually part of control plane)

## Work Plane

- Physical/virtual machines with minimal OS
- **kubelet** + CRI (containerd, CRI-O) for compute
- **kube-proxy** + CNI for networking
- **CSI** controllers for storage
- Extensible for GPUs, virtualization, etc.

## Connecting the Planes

Controllers map desired state (digital twins) to real world (work plane) while reporting actual state back. Work plane can use manually attached machines or automated infrastructure provisioning (e.g., Gardener machine-controller-manager).
