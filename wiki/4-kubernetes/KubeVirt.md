# KubeVirt

**KubeVirt** is a CNCF project that extends Kubernetes with virtualization capabilities, enabling VMs to run alongside containers on the same cluster.

## Overview

KubeVirt adds VM management to Kubernetes through [[KRM]] Custom Resource Definitions and the [[Controller-Pattern]]. It delegates scheduling, networking, and storage to Kubernetes while providing the virtualization layer via libvirt/KVM.

Use cases:
- Legacy workloads that cannot be containerized
- Windows VMs on Kubernetes
- Mixed container + VM environments
- Gradual migration from VMs to containers

## Architecture

KubeVirt uses a service-oriented architecture with choreography:

| Component | Role |
|---|---|
| **virt-api** | API server extension, validates and handles VM-related API requests |
| **virt-controller** | Cluster-wide controller, watches for VM objects and manages VMI lifecycle |
| **virt-handler** | DaemonSet on each node (alongside kubelet), manages VM processes on the host |
| **virt-launcher** | One pod per running VM, wraps the libvirt/QEMU process in a container boundary |

All components run as pods on the cluster — KubeVirt is deployed on top of Kubernetes, not alongside it.

## Core CRDs

| CRD | Purpose |
|---|---|
| `VirtualMachine` (VM) | Persistent, stateful VM definition. Can be stopped/started while preserving data and identity. Similar to a StatefulSet with replicas=1. |
| `VirtualMachineInstance` (VMI) | A running VM instance. Ephemeral — deleting it shuts down the VM. Analogous to a Pod. |
| `VirtualMachineInstanceReplicaSet` (VMIRS) | Group of ephemeral VMIs from a template. Similar to Pod ReplicaSet. |

## VM Lifecycle

Managed via `kubectl` and the `virtctl` CLI:

```bash
# Create a VM
kubectl create -f vm.yaml

# Start / Stop (declarative)
kubectl patch virtualmachine my-vm --type merge -p '{"spec":{"runStrategy":"Always"}}'
kubectl patch virtualmachine my-vm --type merge -p '{"spec":{"runStrategy":"Halted"}}'

# Start / Stop (imperative, with Manual runStrategy)
virtctl start my-vm
virtctl stop my-vm

# Pause / Unpause
virtctl pause vm my-vm
virtctl unpause vm my-vm

# Restart (recreates VMI, picks up config changes)
virtctl restart my-vm

# Delete
kubectl delete virtualmachine my-vm
```

VM states: Stopped, Provisioning, Starting, Running, Paused, Migrating, Stopping, Terminating, Unknown.

## How It Fits

KubeVirt extends the Kubernetes work plane with VM capabilities (see [[Control-Data-Work-Planes]]). It follows the same patterns as native Kubernetes — [[KRM]] for declarative resource definitions, [[Controller-Pattern]] for reconciliation loops. The "KubeVirt Razor" principle: if something is useful for Pods, it should not be implemented only for VMs.

## Links

- [kubevirt.io](https://kubevirt.io/)
- [GitHub — kubevirt/kubevirt](https://github.com/kubevirt/kubevirt)
- [API Reference](https://kubevirt.io/api-reference/)
- [User Guide](https://kubevirt.io/user-guide)
