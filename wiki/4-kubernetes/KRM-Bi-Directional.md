# KRM Bi-Directional Semantics

Actuators read desired state from the resource and actual state from the real world, then align actual to desired. Changes on **either side** may trigger operations.

**Actuators work bi-directionally with the shared repository.**

## Delta-Based, Not Imperative

Unlike imperative REST APIs, [[KRM]] does not issue explicit mutation operations. Operations are determined entirely by the delta between desired and actual state. The real world is simultaneously projected back into resources, making it observable via the control plane.

## Cascading Resources

KRM can be cascaded -- resources create/manipulate other resources, which cascade further. "Real-world element" at the end of the chain is optional.

Example: `Deployment` -> `ReplicaSet` -> `Pod` -> containers. Deployment and ReplicaSet are virtual-only abstractions; only Pod spawns real-world containers.
