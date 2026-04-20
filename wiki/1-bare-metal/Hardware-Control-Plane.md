# Hardware: Control Plane

Minimal control plane footprint for BOS layer and bare metal automation. Does not include capacity for COS layer services (Gardener, etc.) -- add capacity as needed for your target scenario.

## Bare Metal (Single Rack)

Pure bare metal setup for managing hardware without IaaS:

- **3+ management nodes** (HA for orchestration, monitoring, APIs)
- **1 management switch** (interconnects control/work planes)
- **2+ compute nodes** (workload execution, storage)
- **Shared storage** (persistent data, VM images)
- **1+ firewall** (network segmentation)
- **1 console** (out-of-band management)

## CobaltCore (Two Racks)

Bare metal + OpenStack IaaS. Network rack + compute rack.

**Network fabric pod:**
- 3+ spine switches (backbone, 100G QSFP28)
- 2 leaf switches (server connectivity)
- 2+ core switches (external aggregation)
- 2+ firewalls
- 1 management switch (OOB)
- 1+ console server

**Compute pod (8-32 servers):**
- Single/dual-socket (64-144 cores/socket), 256GB-1TB RAM, NVMe SSDs
- 25G/40G/100G NICs, SmartNICs (BlueField, ConnectX)
- 2+ ToR switches, 1 management switch
- Redfish support recommended

## IronCore (Single Rack)

Network, compute, and storage management in one rack.

**Networking:**
- 2+ spine switches (32-port, 100G)
- 2+ leaf/ToR switches (25G/100G)
- OOB management switches + console server
- Router servers (EPYC/Xeon, 192GB+, 3x dual-port 100G NICs)

**Management servers (3+):**
- 32+ cores (EPYC/Xeon)
- 192GB+ RAM
- 3TB+ NVMe SSD
- Dual-port 100G + 10G SFP+ + 1G RJ45
- TPM 2.0, BMC with Redfish
