# Redis Operator

Kubernetes operators for managing Redis deployments with high availability.

## Spotahome Redis Operator

Manages Redis Sentinel deployments on Kubernetes.

- Redis Sentinel for automatic failover
- Configurable Redis and Sentinel settings
- Persistent storage, custom configurations

### CRDs

| CRD | Purpose |
|---|---|
| `RedisFailover` | Redis Sentinel HA deployment |

## OT-CONTAINER-KIT Redis Operator

Manages both Redis Cluster and Redis Sentinel setups.

- Redis Cluster mode (sharding)
- Redis Sentinel mode (HA)
- Standalone mode
- Monitoring with Prometheus exporter

### CRDs

| CRD | Purpose |
|---|---|
| `RedisCluster` | Redis Cluster deployment |
| `RedisReplication` | Redis replication with Sentinel |
| `RedisSentinel` | Sentinel configuration |
| `Redis` | Standalone Redis instance |

## Links

- [GitHub — spotahome/redis-operator](https://github.com/spotahome/redis-operator)
- [GitHub — OT-CONTAINER-KIT/redis-operator](https://github.com/OT-CONTAINER-KIT/redis-operator)
