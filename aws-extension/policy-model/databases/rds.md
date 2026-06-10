---
description: Amazon RDS instances and clusters managed inside an Environment.
---

# RDS

Amazon RDS provides managed relational databases. The AWS Extension supports provisioning both single RDS instances and multi-node Aurora clusters inside an Environment.

## Spec

{% tabs %}
{% tab title="RDS Instance" %}
A single database instance. Suitable for MySQL, PostgreSQL, MariaDB, SQL Server, Oracle, and non-Aurora deployments.

| Field | Description |
|---|---|
| **Engine** | Database engine: MySQL, PostgreSQL, MariaDB, SQL Server, Oracle, Aurora MySQL, Aurora PostgreSQL |
| **Engine Version** | The database engine version |
| **Instance Class** | The compute and memory capacity (e.g. `db.t3.medium`) |
| **Storage** | Allocated storage size in GB and type (gp2, gp3, io1) |
| **Multi-AZ** | Deploy a standby replica in a different AZ for high availability |
| **Database Name** | The initial database name |
| **Username** | The master username |
| **Backup Retention** | Number of days to retain automated backups (0 to disable) |
| **Encryption** | Enable encryption at rest using the Environment's KMS key |
{% endtab %}

{% tab title="Aurora Cluster" %}
A multi-node Aurora cluster with a writer endpoint and one or more reader endpoints.

| Field | Description |
|---|---|
| **Engine** | Aurora MySQL or Aurora PostgreSQL |
| **Engine Version** | The Aurora engine version |
| **Instance Class** | The instance class for cluster nodes |
| **Number of Instances** | Total number of instances (writer + readers) |
| **Database Name** | The initial database name |
| **Backup Retention** | Days to retain automated backups |
| **Encryption** | Enable encryption at rest |
{% endtab %}
{% endtabs %}

## Dependencies

RDS resources require an **Environment**. The Environment's Network Baseline must have RDS subnet groups available (created automatically during network provisioning).
