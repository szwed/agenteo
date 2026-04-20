# MySQL Operator

Kubernetes operators for managing MySQL clusters.

## MySQL Operator for Kubernetes (Oracle)

Official Oracle operator for MySQL InnoDB Cluster on Kubernetes.

- Manages InnoDB Cluster with Group Replication
- Automated provisioning, scaling, backup/restore
- MySQL Router integration for transparent routing

### CRDs

| CRD | Purpose |
|---|---|
| `InnoDBCluster` | MySQL InnoDB Cluster definition |
| `MySQLBackup` | Backup configuration and scheduling |

## Percona Operator for MySQL

Community and enterprise operator from Percona for Percona XtraDB Cluster and MySQL Group Replication.

- Synchronous replication via Percona XtraDB Cluster
- Automated backups (S3, GCS, Azure)
- ProxySQL and HAProxy for load balancing
- Point-in-time recovery

## Links

- [GitHub — mysql/mysql-operator](https://github.com/mysql/mysql-operator)
- [GitHub — percona/percona-xtradb-cluster-operator](https://github.com/percona/percona-xtradb-cluster-operator)
