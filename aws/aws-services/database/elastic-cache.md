---
description: Create ElastiCache for Redis database and Memcache memory caching
---

# Amazon ElastiCache

[Amazon ElastiCache](https://aws.amazon.com/elasticache/features/) is a serverless, Redis- and Memcached-compatible caching service delivering real-time, cost-optimized performance for modern applications.

## Creating an ElastiCache in the DuploCloud Portal

1. In the DuploCloud Portal, navigate to **DevOps** -> **Database.**
2. Click the **ElastiCache** tab.
3. Click **Add**. The **Create a ElastiCache** page displays.
4. Select the ElastiCache **Type** and complete the required fields based on your type selection.
5. Optionally, select **Enable Cluster Mode** to scale the ElastiCache instance for performance.
6. Click **Create**.

<figure><img src="../../../.gitbook/assets/elastic1 (1).png" alt=""><figcaption><p><strong>Create a ElastiCache</strong> page in the DuploCloud Portal</p></figcaption></figure>

{% hint style="info" %}
Pass the cache endpoint to your application through the [Environment Variables](../containers/passing-config-and-secrets.md) via the AWS Service.
{% endhint %}
