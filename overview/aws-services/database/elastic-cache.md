---
description: Create ElastiCache for Redis database and Memcache memory caching
---

# AWS ElastiCache

[Amazon ElastiCache](https://aws.amazon.com/elasticache/features/) is a serverless caching service delivering real-time, cost-optimized performance for modern applications. DuploCloud supports ElastiCache instances of the following types:

* **Memcached**
* **Redis**
* **Valkey**

## Creating a Memcached ElastiCache Instance

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database.**
2.  Select the **ElastiCache** tab, and click **Add**. The **Create a ElastiCache** page displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/memcache.png" alt=""><figcaption><p>The <strong>Create an ElastiCache</strong> page in the DuploCloud Portal</p></figcaption></figure></div>
3. Enter a database **Name**.
4. Specify the number of **Replicas**.&#x20;
5. In the **Type** list box, select **Memcached.**
6. Select the **Memcached Version**.&#x20;
7. Select the node size in the **Size** list box.
8. Click **Create**. The Memcached ElastiCache instance is created.

{% hint style="info" %}
Pass the cache endpoint to your application through the [Environment Variables](../containers/passing-config-and-secrets.md) via the AWS Service.
{% endhint %}

## Creating a Redis or Valkey ElastiCache Instance

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database**.
2. Select the **ElastiCache** tab, and click **Add**. The **Create an ElastiCache** page displays.

<figure><img src="../../../.gitbook/assets/create a redis (1).png" alt=""><figcaption><p>The <strong>Create</strong> <strong>an ElastiCache</strong> page in the DuploCloud Portal</p></figcaption></figure>

3. Enter a database **Name**.
4. Specify the number of **Replicas**.
5. Optionally, enable **Automatic Failover**: if the primary node in the cluster fails, one of the read replicas is automatically promoted. This setting requires at least two replicas.
6. Optionally, enable **Cluster Mode** and specify the **No Of Shards**.&#x20;
7. In the **Type** field, select **Redis** or **Valkey**.
8. In the **Size** list box, select the node size.
9. Optionally, complete the following fields:
   * **Redis Version** or **Valkey Version**: Select the version number of the cache engine to be used. If not set, defaults to the latest version.
   * **Parameter Group Name**: Specify the name of the parameter group to associate with this cache cluster.
   * **KMS**: Select the KMS key.
   * **Encryption At Transit**: Select if Encryption At Transit is needed.
10. Optionally, complete the snapshot fields to configure backup:&#x20;
    * **Snapshot Name:** Select the snapshot/backup you want to use for creating Redis/Valkey.
    * **Snapshot ARNs**: Specify the ARN of a Redis RDB snapshot file stored in Amazon S3. Example- `arn:aws:s3:::s3-backup-foldername/backupobject.rdb`
    * **Snapshot Retention Limit:** Specify retention limit in days. Accepted values - 1-35.
    * **Snapshot Window Start Time**: The time when your automated snapshot process will begin.
    * **Snapshot Window Duration in hours**: The length of time allowed for taking the snapshots automatically.

<div align="left"><figure><img src="../../../.gitbook/assets/image (15) (1).png" alt="" width="563"><figcaption><p>The Snapshot fields on the <strong>Create an ElastiCache</strong> pane</p></figcaption></figure></div>

11. Optionally, click the **CloudWatch** link above the **Log Delivery Configuration** field to enable exporting engine logs and slow logs to Amazon CloudWatch Logs.&#x20;
    * Complete the fields to configure CloudWatch:&#x20;
      * **Log Format**&#x20;
      * **Log Type**&#x20;
      * **Log Group**
    * Click **Add Config**. The configuration is added to the **Log Delivery Configuration** field.

<div align="left"><figure><img src="../../../.gitbook/assets/cloudwatch logs pane.png" alt="" width="350"><figcaption><p>The <strong>Add CloudWatch Logs: Log Delivery Configuration</strong> pane</p></figcaption></figure></div>

12. Click **Create**. The Redis or Valkey database instance is created.

## Troubleshooting Redis Connection Issues in AWS

When a Redis instance in an AWS environment is experiencing connection issues, ensure the Security Group (SG) configuration allows VPN traffic to port `6379`. Then, using the `nc` command, verify the Redis instance's accessibility.

If you encounter local DNS resolution problems, consider changing your DNS provider or connecting directly using the Redis instance's IP address, which can be obtained via the `dig` command.&#x20;

For persistent DNS issues, resetting your router or using external DNS query tools may help. If other troubleshooting steps fail, exploring [AWS network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) can offer additional insights.
