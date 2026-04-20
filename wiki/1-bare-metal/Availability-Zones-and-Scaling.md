# Availability Zones and Scaling

## Availability Zones

Single control/work plane = limited SLAs. For higher resilience, deploy **3 availability zones** -- isolated locations with independent power, cooling, and networking.

Each AZ is a full copy of control + work plane. Requires load balancing across zones and data replication for consistency during zone failure.

## Scaling

### Control Plane

- **Vertical** -- upgrade to more powerful nodes (CPU, memory, storage)
- **Horizontal** -- add racks/nodes for increased capacity and redundancy
- Scale proactively (hardware refresh cycles) or reactively (demand surges)

### Work Plane

- **Horizontal scale-out** -- add compute, storage, network, or AI nodes on demand
- Near-linear throughput increase, seamless integration of new nodes
