# Data and Control Plane State

Control plane state is fully captured within the data plane (persisted in etcd). Three backup approaches:

1. **Data/config files** -- secure etcd or RDBMS files directly
2. **Snapshots** -- capture underlying volume/block-storage (potentially quiescing the database)
3. **API-level** -- save logical Kubernetes resources via API; technology-independent and fully portable

Tools: [Velero](https://velero.io/), [k8up](https://k8up.io/) (CNCF).

## Live Migration

Move a cluster's control plane from one hosting cluster to another -- crucial for maintenance, regional failovers, infrastructure transitions. Non-negotiable principle: continuous availability of the managed cluster. Gardener has specific [migration documentation](https://gardener.cloud/docs/gardener/extensions/migration/) for extension maintainers.

## Pivoting

Enabled by recursive nature of planes. After setting up data/control plane in a bootstrap cluster (donor cloud or laptop) connected to a remote work plane, pivoting moves state and planes into the remote work plane -- handing management to itself (self-reliable).

Solves the **chicken-and-egg problem**: using declarative K8s API to create the very cluster being managed.

Tools:
- **clusterctl** (Cluster API) -- `clusterctl move` command for pivoting
- **gardenadm** (Gardener) -- `bootstrap` command using KinD with automatic pivot

### How `clusterctl move` Works

The `clusterctl move --to-kubeconfig=<target>` command migrates all [[Cluster-API]] objects from a source management cluster to a target. Key behaviors:

- **Namespace targeting** -- use `--namespace` to move only objects from a specific namespace (defaults to current namespace)
- **Pause/resume** -- before moving, sets `Cluster.Spec.Paused=true` on the source to halt reconciliation; waits for any `clusterctl.cluster.x-k8s.io/block-move` annotations to clear; the target cluster resumes reconciliation automatically after move completes
- **Dry-run** -- `--dry-run` prints what would be moved without taking action (use `-v` for verbosity levels)
- **Status not restored** -- object Status subresources are never migrated; controllers on the target rebuild status by observing current state
- **Not a backup tool** -- `clusterctl move` assumes a stable cluster; it is not designed for backup/restore during upgrades or remediations
