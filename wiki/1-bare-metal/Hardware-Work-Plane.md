# Hardware: Work Plane

Specs shared between CobaltCore and IronCore. Adapt based on actual workload profiles.

## Compute

- 128+ cores (single-socket Xeon/EPYC), 512GB+ RAM
- NVMe SSD (1TB+), dual 100G SmartNICs (BlueField-3, ConnectX)
- 1G Base-T for management
- ~16 nodes per 10kW rack

## Storage

- 32-64 cores, 256-512GB RAM
- 8-24 NVMe drives (8-16TB each) for bulk storage
- 1TB+ NVMe boot drive
- Dual 100G QSFP28, 1G management
- SmartNICs optional (cost-sensitive deployments)
- ~12-18 nodes per 10kW rack

## Mixed (Compute + Storage)

Combined racks with modular scaling. Storage nodes with SmartNICs/DPUs, compute nodes with dual-CPU configs (up to several TB RAM). TPM + Redfish standard.

## Network

CobaltCore: dedicated network pod. IronCore: network on compute nodes.

Network pod components: 2-4 ToR switches (25/40/100/400G), tenant switches, 2 load balancers, console access, management switch.

## AI Training

- GPUs: NVIDIA H100, H200, A100 or AMD MI300 (40-141GB HBM per GPU)
- CPU: Xeon/EPYC for preprocessing
- 512GB+ RAM, NVMe SSDs
- 100G QSFP28 / InfiniBand
- Mixed-precision (FP8, FP16), MIG support

## AI Inference

- GPUs: NVIDIA L40S, A100, H100 (24-48GB GDDR6/HBM, up to 8 per node)
- 64+ core CPU, 256GB-1TB RAM
- 25G/100G Ethernet or InfiniBand
- Up to 32 GPUs per rack
