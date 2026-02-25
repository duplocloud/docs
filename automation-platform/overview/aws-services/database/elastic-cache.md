---
description: Create ElastiCache for Redis database and Memcache memory caching
---

# AWS ElastiCache

[Amazon ElastiCache](https://aws.amazon.com/elasticache/features/) is a serverless caching service delivering real-time, cost-optimized performance for modern applications. DuploCloud supports Memcached, Redis, and Valkey ElastiCache instances, including a Serverless Valkey option.

## Creating a Memcached ElastiCache Instance

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database.**
2.  Select the **ElastiCache** tab and click **Add**. The **Create a ElastiCache** page displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (1035).png" alt=""><figcaption><p>The <strong>Create a ElastiCache</strong> page in the DuploCloud Portal</p></figcaption></figure></div>
3. Enter a database **Name**.
4. In the **Type** list box, select **Memcached.**
5. Select the **Memcached Version**.&#x20;
6. Select the node size in the **Size** list box.
7. Specify the number of **Replicas**.&#x20;
8. Click **Create**. The Memcached ElastiCache instance is created.

{% hint style="info" %}
Pass the cache endpoint to your application through the [Environment Variables](../containers/passing-config-and-secrets.md) via the AWS Service.
{% endhint %}

## Creating a Redis or Valkey ElastiCache Instance

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database**.
2. Select the **ElastiCache** tab and click **Add**. The **Create an ElastiCache** page displays.

<figure><img src="../../../../.gitbook/assets/Screenshot (1037).png" alt=""><figcaption><p>The <strong>Create</strong> <strong>an ElastiCache</strong> page in the DuploCloud Portal</p></figcaption></figure>

3. Complete the following fields as required for your Redis or Valkey instance:

<table data-header-hidden><thead><tr><th width="225.5555419921875">Field</th><th>Instruction / Description</th></tr></thead><tbody><tr><td>Serverless</td><td>Select <strong>Yes</strong> or <strong>No</strong> to enable serverless mode.</td></tr><tr><td>Name</td><td>Enter a unique name for the cache. DuploCloud suggests using the tenant name as a prefix.</td></tr><tr><td>Type</td><td>Select <strong>Redis</strong> or <strong>Valkey</strong> from the dropdown.</td></tr><tr><td>Version</td><td>Select the appropriate Redis or Valkey version.</td></tr><tr><td>Size</td><td>Select the instance size for the cluster.</td></tr><tr><td>Log Delivery Configuration</td><td>Select or configure log delivery options.</td></tr><tr><td>Parameter Group Name</td><td>Enter a parameter group for the cluster.</td></tr><tr><td>Replicas</td><td>Specify the initial number of cache nodes that the cache cluster will have.</td></tr><tr><td>Automatic Failover</td><td>Enable or disable automatic failover to the secondary datastore if the primary region becomes unavailable.</td></tr><tr><td>Enable Cluster Mode</td><td>Enable to create Redis in Cluster mode.</td></tr><tr><td>KMS (Optional)</td><td>Select a KMS key for encryption if needed.</td></tr><tr><td>Encryption At Transit</td><td>Select if Encryption At Transit is needed.</td></tr><tr><td>Encryption At Rest</td><td><strong>Valkey only</strong> – Enable/disable encryption of data stored on disk using AWS-managed keys. Recommended for protecting sensitive data at rest.</td></tr><tr><td>Snapshot Name</td><td>Enter a name for a snapshot if desired.</td></tr><tr><td>Snapshot ARNs</td><td>Specify the ARN of a Redis RDB snapshot file stored in Amazon S3. Example- <code>arn:aws:s3:::s3-backup-foldername/backupobject.rdb</code></td></tr><tr><td>Snapshot Retention Limit</td><td>Enter the number of days to retain snapshots.</td></tr><tr><td>Snapshot Window Start Time</td><td>Enter the start time for the snapshot window (e.g., <code>12:00</code>).</td></tr><tr><td>Snapshot Window Duration (Hours)</td><td>Specify the duration of the snapshot window in hours.</td></tr></tbody></table>

<div align="left"><figure><img src="../../../../.gitbook/assets/image (15) (1).png" alt="" width="563"><figcaption><p>The Snapshot fields on the <strong>Create an ElastiCache</strong> pane</p></figcaption></figure></div>

4. Click **Create** to create the Reds or Valkey instance.&#x20;

## Updating Snapshot Retention Limit

After a Redis or Valkey (standard) ElastiCache instance is created, most settings cannot be changed without deleting and recreating the instance. However, you can update the Snapshot Retention Limit at any time.

{% hint style="warning" %}
This setting is not available for Memcached or Valkey Serverless. It applies only to Redis and standard Valkey instances.
{% endhint %}

To update the Snapshot Retention Limit:

1. Navigate to **Cloud Services** -> **Database**.
2. Select the **ElastiCache** tab.
3. Click on the name of the ElastiCache instance in the **NAME** column.&#x20;
4.  Click **Actions**, and select **Update Snapshot Retention Limit**. The **Update Snapshot Retention Limit** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (767).png" alt=""><figcaption><p><strong>Update Snapshot Retention Limit</strong> pane</p></figcaption></figure></div>
5. Select the desired **Snapshot Retention Limit (Days)** (between **1** and **35**).
6. Click **Update** to save your changes.

## **Creating a Serverless Valkey ElastiCache Instance**

Serverless Valkey clusters automatically scale based on workload demand. Unlike standard Redis or Valkey clusters, node size, replicas, and cluster mode are automatically managed by the system.

To create a Serverless Valkey instance, complete the following steps:

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Database** → **ElastiCache**
2. Click **Add**. The **Create a ElastiCache** page displays.
3.  Select the **Serverless** option at the top of the page.<br>

    <figure><img src="../../../../.gitbook/assets/Screenshot (1036).png" alt=""><figcaption></figcaption></figure>
4. &#x20;Complete the following fields:

<table data-header-hidden><thead><tr><th width="194.89642333984375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the Valkey Serverless cluster.</td></tr><tr><td><strong>Type</strong></td><td>Displays <code>Valkey</code>; no action needed as the cache engine is pre-selected.</td></tr><tr><td><strong>Valkey Version</strong></td><td>Select the version of the Valkey cache engine to deploy.</td></tr><tr><td><strong>KMS</strong></td><td>Select the KMS key to use for encryption at rest (e.g., <code>duploservices-sa-4nov</code>).</td></tr><tr><td><strong>Description</strong></td><td>Optionally enter a description for the cluster to help identify it.</td></tr></tbody></table>

5. Click **Create**. DuploCloud provisions the Serverless Valkey cluster automatically and the system manages scaling, availability, and endpoints.

{% hint style="info" %}
Node size, number of replicas, and cluster mode fields are automatically managed and do not require configuration.
{% endhint %}

## Creating an ElastiCache Global Datastore

DuploCloud supports ElastiCache Global Datastores, which allow you to replicate standard Redis and standard Valkey clusters across multiple AWS regions. Memcached and Serverless Valkey clusters are not supported for Global Datastores.

### Creating a Global Datastore

When you create a Global Datastore in DuploCloud, a primary Redis cluster in the current Tenant and a secondary cluster in a different region are created automatically. You can add additional secondary clusters in other regions as necessary.

1. Navigate to to **Cloud Services** → **Database** → **ElastiCache** → **Global Datastores**.
2.  Click **Add**. The **Create a Global Datastore** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (868).png" alt=""><figcaption><p><strong>Create a Global Datastore</strong> pane </p></figcaption></figure></div>
3. Complete the fields, as required for your configuration:

<table data-header-hidden><thead><tr><th width="218.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the datastore. We recommend using the Tenant name as a prefix.</td></tr><tr><td><strong>Redis Version</strong></td><td>Select the Redis version to deploy.</td></tr><tr><td><strong>Size</strong></td><td>Select a node size. Only Large or larger nodes are supported, and burstable types (t-class) are not allowed.</td></tr><tr><td><strong>Global Replication Group</strong></td><td>Enter a name for the replication group.</td></tr><tr><td><strong>Global Replication Group Description</strong></td><td>Optionally, enter a description for the replication group.</td></tr><tr><td><strong>Secondary Cluster Region</strong></td><td>Select the Tenant/region where you want the secondary cluster to reside.</td></tr><tr><td><strong>Log Delivery Configuration</strong>  </td><td>Configure a log destination to capture Redis logs for monitoring and troubleshooting.</td></tr><tr><td><strong>Parameter Group Name</strong></td><td>Select the parameter group name for log delivery.</td></tr><tr><td><strong>Replicas</strong></td><td>Enter the number of replicas.</td></tr><tr><td><strong>No of Shards</strong></td><td>Specify the number of shards for the cluster.</td></tr><tr><td><strong>KMS (Optional)</strong></td><td>Select a KMS key to enable server-side encryption for the Global Datastore.</td></tr><tr><td><strong>Encryption in Transit</strong></td><td><p>Enable or disable in-transit encryption.</p><ul><li>When enabled, enter the password clients will use to authenticate to the cluster in the <strong>Auth Token (Optional)</strong> field.</li></ul></td></tr><tr><td><strong>Secondary Cluster KMS</strong></td><td>Select a KMS key to enable server-side encryption for any secondary clusters you add.</td></tr><tr><td><strong>Snapshot Retention Limit</strong></td><td>Enter retention period in days.</td></tr><tr><td><strong>Snapshot Window Start Time</strong></td><td>Enter the start time for the snapshot window.</td></tr><tr><td><strong>Snapshot Window Duration in Hours</strong></td><td>Enter the duration of the snapshot window in hours.</td></tr></tbody></table>

4. Click **Create** to provision the ElastiCache Global Datastore.

### Adding Regional Clusters

After creating a Global Datastore, you can add secondary clusters (regional clusters) to replicate the primary Redis cluster across other AWS regions.

1. Navigate to **Cloud Services** → **Databases** → **ElastiCache** → **Global Datastores**.
2. Select the **Regional Clusters** tab.
3.  Click **Add**. The **Add Secondary Cluster** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (871).png" alt=""><figcaption><p><strong>Add Secondary Cluster</strong> pane</p></figcaption></figure></div>
4. Complete the following fields:

<table data-header-hidden><thead><tr><th width="177.3333740234375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the secondary cluster.</td></tr><tr><td><strong>Description</strong></td><td>Optionally, enter a description for the cluster.</td></tr><tr><td><strong>Tenant</strong></td><td>Select the Tenant that will own this secondary cluster.</td></tr><tr><td><strong>KMS</strong> (Optional)</td><td>If a KMS key was selected when creating the Global Datastore, select the same KMS key to enable server-side encryption for the secondary cluster.</td></tr><tr><td><strong>Auth Token</strong> (Optional)</td><td>If a KMS key was selected when creating the Global Datastore, enter the authentication token for client connections.</td></tr></tbody></table>

5. Click **Create** to provision the secondary cluster.

{% hint style="info" %}
Each regional cluster added becomes a read replica of the primary Redis cluster. You can retrieve the primary or secondary cluster endpoint directly from the **Redis Cluster** tab to connect your application.
{% endhint %}

### Viewing Cluster Details

To view cluster details, including connection endpoints for a Global Datastore:

1. Navigate to **Cloud Services** → **Database** → **ElastiCache** → **Global Datastores**.
2. Select the name of the Global Datastore.
3. Select the **Regional Clusters** tab. A list of clusters in the Global Datastore displays.
4. Click the name of the cluster you want to view details for.
5. Use the tabs to explore cluster details:&#x20;

<table data-header-hidden><thead><tr><th width="143.77777099609375">Tab</th><th>Description</th></tr></thead><tbody><tr><td><strong>Redis Cluster</strong></td><td>Displays cluster details, including the endpoint. </td></tr><tr><td><strong>Details</strong></td><td>Shows a JSON representation of the cluster configuration and status.</td></tr><tr><td><strong>Alerts</strong></td><td>Displays any alerts related to the cluster.</td></tr><tr><td><strong>Snapshots</strong></td><td>Lists available snapshots and backup information for the cluster.</td></tr></tbody></table>

{% hint style="info" %}
Each cluster provides a single endpoint. The primary endpoint handles **write operations**, and the secondary endpoint handles **read operations**.&#x20;
{% endhint %}

<figure><img src="../../../../.gitbook/assets/Screenshot (870).png" alt=""><figcaption><p>Cluster detail page with <strong>Redis Cluster</strong>, <strong>Details</strong>, <strong>Alerts</strong>, and <strong>Snapshots</strong> tabs.</p></figcaption></figure>

### Removing Clusters

To remove a cluster from a Global Datastore:

1. Navigate to **Cloud Services** → **Database** → **ElastiCache** → **Global Datastores**.
2. Select the name of the Global Datastore.
3. Select the **Regional Clusters** tab
4. Click the menu icon (<img src="../../../../.gitbook/assets/menu icon (19) (2).avif" alt="" data-size="line">) in the row of the cluster you want to remove.
5. Select **Remove**.

{% hint style="warning" %}
**Important:**

* Secondary clusters must be removed **before** the primary cluster.
* Once all secondary clusters are removed, the primary cluster can be removed.
* Any removed cluster becomes a **standalone cluster**.
{% endhint %}

## Troubleshooting Redis Connection Issues in AWS

When a Redis instance in an AWS environment is experiencing connection issues, ensure the Security Group (SG) configuration allows VPN traffic to port `6379`. Then, using the `nc` command, verify the Redis instance's accessibility.

If you encounter local DNS resolution problems, consider changing your DNS provider or connecting directly using the Redis instance's IP address, which can be obtained via the `dig` command.&#x20;

For persistent DNS issues, resetting your router or using external DNS query tools may help. If other troubleshooting steps fail, exploring [AWS network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) can offer additional insights.
