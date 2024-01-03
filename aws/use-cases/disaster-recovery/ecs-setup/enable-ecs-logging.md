---
description: Enable ECS Elasticsearch logging for containers at the Tenant level
---

# Enable ECS logging

To generate logs for AWS ECS clusters, you must first create an Elasticsearch logging container. Once auditing is enabled, your container logging data can be captured for analysis.

## Before you begin

* [Create a Task Definition](../../../aws-services/containers/#7-toc-title)
* Define at least one [service and container](../../../aws-services/containers/).
* Enable the Audit feature.

## Enabl ECS Elastic Search Logging for a Tenant

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenant**. The **Tenant** page displays.
2. From the **Name** column, select the Tenant that is running the container for which you want to enable logging.
3. Click the **Settings** tab.
4. Click **Add**. The **Add Tenant Feature** pane displays.
5. From the **Select Feature** list box, select **Other**. The **Configuration** field displays.
6. In the **Configuration** field, enter **Enable ECS ElasticSearch Logging**.&#x20;
7. In the field below the **Configuration** field, enter **True**.
8. Click **Add**. In the **Settings** tab, **Enable ECS ElasticSearch Logging** displays a **Value** of **True**.&#x20;

<div align="left">

<figure><img src="../../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

</div>

## Verifying ECS logging is enabled&#x20;

You can verify that ECS logging is enabled for a specific container.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Containers** -> **ECS**.
2.  In the **Task Definitions** tab, select the **Task Definition Family Name** in which your container is defined. The Task Definition Family Name detail page displays. In the example below, the Task Definition Family Name is **DUPLOSERVICES-UX-TEAM-BGTD1**.\


    <div align="left">

    <figure><img src="../../../../.gitbook/assets/AWS_ECS_Logging_6.png" alt=""><figcaption><p>The Task Definition Family Name detail page with <strong>Task Defintions</strong> tab</p></figcaption></figure>

    </div>


3. Click the **Task Definitions** tab.
4. In the **Task Definitions tab**, click the Edit Icon ( <img src="../../../../.gitbook/assets/square_edit_icon (2).png" alt="" data-size="line"> ) to edit the Task Definition. The **Edit Task Definition** page displays your defined **Container**s.

<div align="left">

<figure><img src="../../../../.gitbook/assets/AWS_ECS_Logging_5.png" alt=""><figcaption><p><strong>Task Definitions</strong> Icon (highligted) in Task Definitions tab</p></figcaption></figure>

</div>

In the **Container - 1** area, in the **Container Other Config** field, your `LogConfiguration` is displayed.

<div align="left">

<figure><img src="../../../../.gitbook/assets/AWS_ECS_Logging_3 (1).png" alt=""><figcaption><p><strong>Container - 1</strong> area of the Task Definition editor with highlighted <strong>Container Other Config</strong> field for <strong>container1</strong></p></figcaption></figure>

</div>

In the **Container-2** area, another container is created by DuploCloud with the name `log_router`.

<figure><img src="../../../../.gitbook/assets/image (109).png" alt=""><figcaption><p><strong>Container - 2</strong> area of the Task Definition editor displaying configuration for <strong>log_router</strong> container, created by DuploCloud</p></figcaption></figure>
