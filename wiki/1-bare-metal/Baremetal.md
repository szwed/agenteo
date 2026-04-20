# Baremetal

Traditional baremetal management relies on imperative workflows, custom scripting, manual BMC interventions, and vendor-specific tools. Apeiro replaces this with a cloud-native control plane for the entire physical lifecycle: discovery, provisioning, and day-2 operations (BIOS updates, firmware, inventory) -- all declarative.

## IronCore Baremetal Automation

IronCore uses the Kubernetes API and Resource Model (KRM) as a generalized platform API for infrastructure automation. Two core concepts:

1. **Out-of-band server management** -- BMC/Redfish-based remote control
2. **In-band server boot automation** -- OS provisioning and configuration

Default (not exclusive) baremetal management provider in ApeiroRA.

## Links

- [IronCore](https://ironcore.dev/)
- [IronCore Baremetal Automation](https://ironcore.dev/baremetal/)
- [IronCore IaaS](https://ironcore.dev/iaas/getting-started.html)
- [IronCore on GitHub](https://github.com/ironcore-dev/)
