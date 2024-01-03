---
description: Set up logging for the DuploCloud Portal
---

# Logging Setup

## Prerequisite: ensure Docker containers use stdout

Before setting up logging, ensure that your Docker applications use `stdout` for writing log files.  This is necessary for Docker to collect logs and place them in the host directory, mount them into [Filebeat ](https://www.elastic.co/beats/filebeat)containers, and send them to [AWS Elasticsearch](https://aws.amazon.com/what-is/elasticsearch/)

## Setting up logging&#x20;

1. In the DuploCloud Portal, navigate to **Administrator** -> **Diagnostics** -> **Settings** -> **Logging**.
2. From the **Tenant** list box at the top of the DuploCloud Portal, select the **Default** Tenant.
3.  Click the **Create Logging** link. The **Enable Logging** page displays.\


    <div align="left">

    <figure><img src="../../../.gitbook/assets/image (2) (2).png" alt=""><figcaption><p><strong>Create Logging</strong> link</p></figcaption></figure>

    </div>


4.  Use the **Enable Logging** page to deploy logging for the Control Plane, which uses Open Search and KIbana to retrieve and display log data for the Default Tenant. In the Cert ARN field, enter the certificate of the ARN for the Default Tenant.\


    <div align="left">

    <figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption><p><strong>Enable Logging</strong> page</p></figcaption></figure>

    </div>


5. Click **Submit**. Data gathering takes about fifteen (15) minutes. When data gathering is complete, graphical logging data is displayed in the Logging tab.&#x20;
6. After logging has been enabled for the Control Plane, finish the logging setup by enabling the Log Collector to collect logs per Tenant. This feature is useful for Tenants that are spread across multiple regions and the administrator wants to create a separate logging setup. In the DuploCloud Portal, navigate to **Administrator** -> **Diagnostics** -> **Settings**. &#x20;
7.  In the **Logging** tab, on the **Logging Infrastructure Tenants** page, click **Add.**\


    <figure><img src="../../../.gitbook/assets/image (1) (4).png" alt=""><figcaption><p><strong>Add</strong> button on the <strong>Logging Infrastructure Tenants</strong> page</p></figcaption></figure>
8.  Select the Tenants for which you want to configure logging, as in the example below. The Control Plane configuration you previously set up will be deployed for each Tenant you select in the Infrastructure specified in **Infrastructure Details**.\


    ![Logging tab with logging setup complete](<../../../.gitbook/assets/image (15) (1) (1).png>)

{% hint style="info" %}
&#x20;The Log Collector uses Filebeat containers that are deployed within each Tenant. You can view the Filebeat containers by navigating to **DevOps** -> **Containers** -> **EKS/Native** in the DuploCloud Portal and selecting the **Containers** tab.
{% endhint %}

## How DuploCloud configures logging for you

When you perform the steps above to configure logging, DuploCloud does the following for you.

### Control Plan deployment

1. **An EC2 Host is added** in the Default tenant, for example, **duploservices-default-oc-diagnostics**.
2. **Services are added** in the Default tenant, one for OpenSearch and one for Kibana. Both services are pinned to the EC2 host using [allocation tags](../../../extras/creating-advanced-functions.md). Kibana is set up to point to ElasticSearch and exposed using an internal load balancer.
3. **Security rules from within the internal network to port 443 are added** in the Default tenant to allow the log collectors that run on Tenant hosts to send logs to ElasticSearch. &#x20;

### Log Collector deployment

1. A Filebeat service (`filebeat-duploinfrasvc)` is deployed for each Tenant where central logging is enabled.&#x20;
2. The /var/lib/docker/Containers are mounted from the Host into the Filebeat container. The Filebeat container references ElasticSearch, which runs in the Default Tenant. Inside the container, Filebeat is configured so that every log line is added with metadata information comprising the Tenant name, Service names, Container ID, and Host name, enabling ease of searching by these parameters using ElasticSearch.   &#x20;
