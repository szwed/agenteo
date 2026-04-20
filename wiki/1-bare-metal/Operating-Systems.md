# Operating Systems

## Garden Linux

[Garden Linux](https://gardenlinux.io) -- default (not exclusive) OS in ApeiroRA. Debian-based, purpose-built for containers, K8s, and VMs.

### Key Characteristics

- **Minimal** -- only essentials for running containers; small images, fast boot, reduced attack surface
- **Secure by default** -- immutable root filesystem, least privilege, SELinux/AppArmor/seccomp, atomic security updates
- **Atomic and ephemeral** -- atomic upgrades/rollbacks, stateless disposable nodes, dynamic cluster scaling

### Integration

Natively supports containerd/CRI-O, optimized for Kubernetes. Supports cloud-init/Ignition for automated provisioning. Used by Gardener for all [Kubernetes conformance tests](https://testgrid.k8s.io/conformance-gardener).

See also: [Gardener Extension for Garden Linux](https://gardener.cloud/docs/extensions/os-extensions/gardener-extension-os-gardenlinux/)
