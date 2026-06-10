---
description: Managed databases inside an Environment — RDS and ElastiCache.
---

# Databases

The AWS Extension supports provisioning managed databases inside an Environment. Databases are provisioned into the private subnets of the Environment's Network Baseline, using the subnet groups created during network provisioning.

## Database Types

<table data-view="cards">
  <thead>
    <tr>
      <th>Title</th>
      <th>Description</th>
      <th data-card-target data-type="content-ref">Target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>RDS</strong></td>
      <td>Amazon Relational Database Service — MySQL, PostgreSQL, MariaDB, SQL Server, Oracle, and Aurora.</td>
      <td><a href="rds.md">RDS</a></td>
    </tr>
    <tr>
      <td><strong>ElastiCache</strong></td>
      <td>Amazon ElastiCache — Redis and Memcached in-memory data stores.</td>
      <td><a href="elasticache.md">ElastiCache</a></td>
    </tr>
  </tbody>
</table>

## Dependencies

All databases require an **Environment** with an associated **Network Baseline** that has RDS and ElastiCache subnet groups available.

{% hint style="warning" %}
Subnet groups are created automatically during Network Baseline provisioning. Networks attached using **Import** mode may not have subnet groups — provisioning a database into an imported network without them will fail.
{% endhint %}
