---
description: Amazon ElastiCache instances managed inside an Environment — Redis and Memcached.
---

# ElastiCache

Amazon ElastiCache provides managed in-memory data stores for caching and session management. The AWS Extension supports provisioning ElastiCache clusters inside an Environment.

## Spec

| Field | Description |
|---|---|
| **Engine** | **Redis** or **Memcached** |
| **Engine Version** | The ElastiCache engine version |
| **Node Type** | The compute and memory capacity (e.g. `cache.t3.micro`) |
| **Number of Nodes** | Number of cache nodes |
| **Multi-AZ** | Enable automatic failover across AZs (Redis only) |
| **Encryption at Rest** | Encrypt data stored on disk (Redis only) |
| **Encryption in Transit** | Require TLS for all connections |

## Result

| Field | Description |
|---|---|
| **Endpoint** | The connection endpoint for your application |
| **Port** | The port the cluster is listening on |

## Dependencies

ElastiCache requires an **Environment**. The Environment's Network Baseline must have the ElastiCache private subnet group available (created automatically during network provisioning). ElastiCache is provisioned into private subnets only.
