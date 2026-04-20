# MongoDB Operator

Kubernetes operators for managing MongoDB deployments.

## MongoDB Community Operator

Official community operator from MongoDB Inc.

- Manages MongoDB replica sets on Kubernetes
- Automated deployment and scaling
- TLS, SCRAM authentication
- Persistent storage management

### CRDs

| CRD | Purpose |
|---|---|
| `MongoDBCommunity` | MongoDB replica set definition |

## Percona Operator for MongoDB

Enterprise-grade operator from Percona for Percona Server for MongoDB.

- Replica sets and sharded clusters
- Automated backups (S3, GCS, Azure) with point-in-time recovery
- Monitoring integration (PMM)
- Encryption at rest

### CRDs

| CRD | Purpose |
|---|---|
| `PerconaServerMongoDB` | Full MongoDB cluster definition |

## Links

- [GitHub — mongodb/mongodb-kubernetes-operator](https://github.com/mongodb/mongodb-kubernetes-operator)
- [GitHub — percona/percona-server-mongodb-operator](https://github.com/percona/percona-server-mongodb-operator)
