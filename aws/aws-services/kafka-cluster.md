---
description: Create a Kafka Cluster for real-time streaming data pipelines and apps
---

# Kafka Cluster

Apache Kafka (Kafka) is an open-source, distributed streaming platform that enables the development of real-time, event-driven applications. It is used to build real-time streaming data pipelines and real-time streaming applications.&#x20;

A data pipeline reliably processes and moves data from one system to another, and a streaming application is an application that consumes streams of data. Streaming platforms enable developers to build applications that continuously consume and process streams at high speeds, with a high level of accuracy.

For complete documentation on Apache Kafka, see the [AWS documentation](https://docs.aws.amazon.com/msk/latest/developerguide/what-is-msk.html).

## Prerequisites

Before creating a Kafka Cluster. configure the cluster in AWS.&#x20;

DuploCloud uses the Kafka Cluster Name you configured in the AWS Portal to locate and import the **Cluster Configuration** and **Configuration Revision** fields in the DuploCloud **Creating a Kafka Cluster** pane.

## Creating a Kafka Cluster

1. In the DuploCloud Portal, navigate to **DevOps** -> **Analytics**.
2. Click the **Kafka** tab.
3. Click **Add**. The **Create a Kafka Cluster** pane displays.
4. Enter a **Kafka Cluster Name**.
5. From the field list boxes, select a **Version** of Kafka, the **Size** of the cluster you want to create, the **Volume** size in gigabytes, and the **Transit Encryption** mode. The **Cluster Configuration** and **Configuration Revision** fields are populated [if you define the cluster in the AWS Portal](kafka-cluster.md#prerequisites).
6.  Optionally, select **Availability Zones** or **Number of BrokerNodes**. You must specify a minimum of two (2) **Availability Zones** zones.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/kafka_Prereq1 (2).png" alt=""><figcaption><p><strong>Create a Kafka Cluster</strong> pane<br></p></figcaption></figure>

    </div>
7.  Click **Submit**. The cluster is created and displayed as **Active** in the **Kafka** tab. It may take up to half an hour to create the cluster.\


    <div align="left">

    <figure><img src="../../.gitbook/assets/k2.png" alt=""><figcaption><p><strong>Kafka</strong> tab with Kafka clusters<br></p></figcaption></figure>

    </div>

## Viewing Kafka Clusters

View Kafka Clusters by navigating to **DevOps** -> **Analytics** in the DuploCloud Portal and selecting the **Kafka** tab.

## Changing the Configuration of a Kafka Cluster

1. In the DuploCloud Portal, navigate to **DevOps** -> **Analytics**.
2. Click the **Kafka** tab.&#x20;
3. Select the Kafka Cluster with **Active Status** from the **Name** column. The **Kafka Cluster** page displays.&#x20;
4.  Click the **Actions** menu and select **Change Configuration**. The **Change Cluster Configuration** pane displays.\


    <figure><img src="../../.gitbook/assets/kafka_Prereq2.png" alt=""><figcaption><p>Kafka Cluster page <strong>Actions</strong> menu displaying <strong>Change Configuration</strong> option</p></figcaption></figure>


5.  From the **Cluster Configuration** list box, select the new cluster configuration.\


    <figure><img src="../../.gitbook/assets/kafka_Prereq3.png" alt=""><figcaption><p><strong>Change Cluster Configuration</strong> pane .</p></figcaption></figure>


6. From the **Configuration Revision** list box, select the revision of the new cluster configuration.
7. Click **Submit**. The configuration change is displayed on the **Kafka Cluster** page

<figure><img src="../../.gitbook/assets/kafka_Prereq4.png" alt=""><figcaption><p><strong>Kafka Cluster</strong> page with available tabs detailing configuration</p></figcaption></figure>
