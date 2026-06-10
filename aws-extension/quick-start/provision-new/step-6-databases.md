---
description: Add a managed database to your Environment — RDS or ElastiCache.
---

# Step 6: Add Databases

Databases in DuploCloud AI Suite are provisioned inside a Resource Group. The **Databases** section of the resource group sidebar exposes two services: **RDS** (relational database instances and Aurora clusters) and **ElastiCache** (Redis/Valkey and Memcached caches). Both are provisioned via CloudFormation and inherit the resource group's IAM role, KMS key, VPC, and subnet configuration automatically.

Navigate to a resource group and expand **Cloud Resources → Databases** in the sidebar to access both services.

![](<../../../.gitbook/assets/database-step-03.png>)

---

## RDS Instance

### Step 1 — RDS Instances List

In the resource group sidebar, expand **Cloud Resources → Databases → RDS** and select **Instances**. The list shows all RDS instances provisioned under this resource group with their engine, instance class, visibility, Multi-AZ status, and overall status. When starting fresh the list is empty. Click **+ Create RDS Instance** to begin.

![](<../../../.gitbook/assets/database-step-04.png>)

### Step 2 — Basics

The **Create RDS Instance** wizard opens. Fill in the **Basics** page:

- **Name** — used as the AWS `DBInstanceIdentifier` (e.g. `prod-db`)
- **Description** — optional
- **Restore from snapshot** — toggle on to seed from an existing snapshot; engine, version, credentials, and storage size are inherited from the snapshot

Click **Next**.

![](<../../../.gitbook/assets/database-step-05.png>)

### Step 3 — Engine

Configure the database engine:

- **Engine** — the database engine (e.g. `mysql`). The dropdown lists all supported non-cluster engines.
- **Engine Version** — select a version (e.g. `8.4.9`). Versions are cached per region for 6 hours.
- **DB Instance Class** — the RDS instance class (e.g. `db.t3.small`)
- **Initial DB Name** — optional; defaults to the instance name when left blank

Click **Next**.

![](<../../../.gitbook/assets/database-step-06.png>)

### Step 4 — Storage

Configure storage:

- **Allocated Storage (GiB)** — the initial storage allocation (e.g. `20`)
- **Storage Type** — optional; accepts `gp3`, `io1`, or `standard`. Defaults to `gp3`.
- **Storage Encryption** — `Encrypt with Resource Group KMS key` uses the resource group's KMS key (auto-stamped server-side). `AWS default` uses the AWS-managed `aws/rds` key.

Click **Next**.

![](<../../../.gitbook/assets/database-step-07.png>)

### Step 5 — Networking

Configure network placement:

- **Visibility** — `Private (recommended)` places the instance in the network's private RDS subnet group and sets `PubliclyAccessible: false`. `Public` uses public subnets.
- **Availability Zone** — optional; pulled from the parent network's subnets (e.g. `us-east-1a`). Leave blank to let AWS choose.
- **Multi-AZ deployment** — toggle on to provision a standby replica in a second availability zone for high availability

Click **Next**.

![](<../../../.gitbook/assets/database-step-08.png>)

### Step 6 — Auth & Backup

Configure credentials and backup:

- **Master Username** — the database admin account (e.g. `root`)
- **Master Password** — stored encrypted at rest; plaintext is only sent to AWS via the CloudFormation `NoEcho` parameter
- **Backup Retention (days)** — automated backup retention period; `0` disables backups, max 35 days
- **Deletion protection** — prevents accidental deletion of the instance
- **Performance Insights** — enables AWS Performance Insights for query-level monitoring
- **IAM database authentication** — enables IAM-based authentication alongside password auth
- **Custom Parameter Group entries** — optional per-parameter overrides applied to the instance's parameter group

Click **Create & Provision**.

![](<../../../.gitbook/assets/database-step-09.png>)

### Step 7 — Provisioning Started

The RDS instance detail page opens with **Status: Provisioning**. The spec summary confirms the linked resource group, visibility, allocated storage, storage encryption method, and backup retention. Click **Track Provisioning Status** to open the agent ticket and follow provisioning in real time.

![](<../../../.gitbook/assets/database-step-10.png>)

### Step 8 — Agent: Phase 0 — Acknowledge

The agent opens a ticket titled **AWSRdsInstance Resource Management — prod-db** using the `duplo-aws-resources` skill. It reads the RDS instance skill file, checks for the spec file and environment variables, confirms credentials are present, and begins Phase 0 — Acknowledge.

![](<../../../.gitbook/assets/database-step-11.png>)

### Step 9 — Agent: Validate & Prepare

The agent runs Phase 0.3 (AWS_PROFILE guard), Phase 1 (validate context), and derives the parameter group family and CloudFormation stack name from the instance spec. It then merges any custom parameter group entries into the CloudFormation template.

![](<../../../.gitbook/assets/database-step-12.png>)

### Step 10 — Agent: CloudFormation Submitted

The agent installs the `ruamel.yaml` library used for template merging, merges the CloudFormation template, and submits the stack in Phase 2. It then polls stack events in real time, reporting each resource as it is created.

![](<../../../.gitbook/assets/database-step-14.png>)

### Step 11 — Agent: Provisioning Complete

The stack reaches `CREATE_COMPLETE`. The agent posts the final provisioning summary confirming the RDS instance ARN, DB instance identifier, engine and version, instance class, allocated storage, availability zone, endpoint URL, and status.

![](<../../../.gitbook/assets/database-step-15.png>)

### Step 12 — RDS Instance Ready

The instance detail page updates to **Status: Ready**. The **Overview** tab shows all key instance details:

- **Engine** / **Engine Version** / **Instance Class**
- **AWS Status**: available / **Port** / **Availability Zone**
- **Multi-AZ** and **Publicly Accessible** flags
- **Endpoint** — the connection hostname for the instance
- **CloudFormation Stack** — the ARN of the stack managing all provisioned resources

Additional tabs — **Storage**, **Networking**, and **Parameters** — provide the full storage configuration, subnet and security group assignments, and any applied parameter group entries.

![](<../../../.gitbook/assets/database-step-16.png>)

---

## RDS Cluster

{% hint style="info" %}
RDS Cluster support (Aurora MySQL and Aurora PostgreSQL) is coming soon.
{% endhint %}

---

## ElastiCache

### Step 1 — ElastiCache List

In the resource group sidebar, expand **Cloud Resources → Databases** and select **ElastiCache**. The list shows all ElastiCache clusters provisioned under this resource group with their engine, cluster mode, topology, and status. When starting fresh the list is empty. Click **+ Create ElastiCache** to begin.

![](<../../../.gitbook/assets/database-step-35.png>)

### Step 2 — Basics

The **Create ElastiCache** wizard opens. Fill in the **Basics** page:

- **Name** — used as the AWS `ReplicationGroupId` (Redis/Valkey) or `CacheClusterId` (Memcached), e.g. `prod-db-cache`
- **Description** — optional

Click **Next**.

![](<../../../.gitbook/assets/database-step-36.png>)

### Step 3 — Engine

Configure the cache engine:

- **Engine** — `Redis`, `Valkey`, or `Memcached`
- **Engine Version** — the version to deploy (e.g. `7.0`)
- **Cache Node Type** — the node instance class (e.g. `cache.t3.small`)
- **Port** — the port the cache listens on (default `6379` for Redis/Valkey)
- **Restore source** — `None (fresh)` for a new cluster; select `ElastiCache snapshot` or `S3 RDB seed` to restore from an existing backup. The engine version is inherited from the snapshot when restoring.

Click **Next**.

![](<../../../.gitbook/assets/database-step-37.png>)

### Step 4 — Topology

Configure the cluster topology:

- **Cluster Mode** — `Disabled` (single shard, primary + replicas) or `Enabled` (multiple shards for horizontal scaling)
- **Number of Cache Clusters** — sets the total node count (1 primary + N replicas). Selecting more than 1 automatically enables Multi-AZ and Automatic Failover.

Click **Next**.

![](<../../../.gitbook/assets/database-step-38.png>)

### Step 5 — Encryption & Auth

Configure encryption and authentication:

- **At-Rest Encryption** — `Resource Group KMS key (recommended)` uses the resource group's KMS key. Other options use AWS-managed keys.
- **Transit Encryption (TLS)** — toggle on to require TLS for all client connections

Click **Next**.

![](<../../../.gitbook/assets/database-step-39.png>)

### Step 6 — Backup & Maintenance

Configure backup and maintenance windows:

- **Snapshot Retention (days)** — number of days to retain automatic snapshots; `0` disables snapshots
- **Snapshot Window (UTC)** — optional preferred time window for taking daily snapshots
- **Maintenance Window (UTC)** — optional preferred window for applying minor patches; should not overlap the snapshot window
- **Auto Minor Version Upgrade** — automatically applies minor engine version upgrades during the maintenance window
- **Data Tiering** — enables SSD data tiering for `cache.r6gd.*` node types only
- **Parameter Group Overrides** — optional per-parameter overrides

Click **Create**.

![](<../../../.gitbook/assets/database-step-44.png>)

### Step 7 — Provisioning Started

The ElastiCache detail page opens with **Status: Provisioning**. The spec summary confirms the linked resource group, cluster mode, snapshot retention, and at-rest encryption method. Click **Track Provisioning Status** to open the agent ticket.

![](<../../../.gitbook/assets/database-step-46.png>)

### Step 8 — Agent: Phase 0 & Phase 0.5

The agent opens a ticket titled **AWSElastiCache Resource Management — prod-db-cache** using the `duplo-aws-resources` skill. It reads the ElastiCache skill file and spec file, then runs Phase 0 (Acknowledge) and Phase 0.5 (AWS_PROFILE guard + credential check).

![](<../../../.gitbook/assets/database-step-47.png>)

### Step 9 — Agent: Phase 1 — Preflight & Validate

The agent runs four Phase 1 sub-steps:

- **Phase 1 — Preflight**: exports AWS credentials and profile
- **Phase 1.2 — Validate context**: confirms all required spec fields are present and well-formed
- **Phase 1.3 — Derive parameter group family + stack name**: resolves the ElastiCache parameter group family and derives the CloudFormation stack name
- **Phase 1.4 — Merge custom parameter-group entries**: applies any custom parameter overrides into the CloudFormation template

![](<../../../.gitbook/assets/database-step-48.png>)

### Step 10 — Agent: CloudFormation Submitted

The agent merges the template in a single shell session to maintain environment state, confirms no pre-existing stack, and submits the CloudFormation stack in Phase 2. It then polls stack events in real time until the stack completes.

![](<../../../.gitbook/assets/database-step-49.png>)

### Step 11 — Agent: Provisioning Complete

The stack reaches `CREATE_COMPLETE`. The agent posts the final provisioning summary:

| Field | Value |
|---|---|
| Engine | Redis 7.0 |
| Node type | cache.t3.small |
| Cluster mode | Disabled (2 nodes: 1 primary + 1 replica) |
| At-rest encryption | Enabled (KMS key) |
| Transit encryption | Disabled |
| Status | Complete |

![](<../../../.gitbook/assets/database-step-51.png>)

### Step 12 — ElastiCache Ready

The detail page updates to **Status: Ready**. The **Overview** tab shows all key cluster details:

- **Engine** / **Engine Version** / **Cluster Mode**
- **AWS Status**: available / **Port** / **Cache Node Type**
- **Primary Endpoint** — the write endpoint for the replication group
- **Reader Endpoint** — the read-only endpoint that load-balances across replicas
- **CloudFormation Stack** — the ARN of the stack managing all provisioned resources

![](<../../../.gitbook/assets/database-step-52.png>)

### Step 13 — Cache Clusters

The **Cache Clusters** tab shows the full shard and node topology. The **Shards / Node Groups** table lists each shard with its status, primary endpoint, and reader endpoint. The **Cache Cluster Nodes** table lists individual nodes with their cluster ID, node type, status, availability zone, engine, and version.

![](<../../../.gitbook/assets/database-step-53.png>)
