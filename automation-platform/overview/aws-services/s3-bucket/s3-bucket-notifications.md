---
description: Creating S3 bucket notifications in DuploCloud
---

# S3 Bucket Notifications

DuploCloud makes it easy to configure event-driven workflows using Amazon S3 bucket notifications. You can trigger SQS queues, SNS topics, or Lambda functions automatically when specific events occur in an S3 bucket, such as when a new object is uploaded or deleted.

Before setting up a notification, ensure the destination resource (SQS, SNS, or Lambda) is available in your Tenant. For help creating these resources, see:

* [SQS Queues](../sqs-queue.md#creating-sqs-queues): for receiving event messages asynchronously.
* [SNS Topics](../sns-topic.md#creating-a-sns-topic): for publishing notifications to multiple subscribers.
* [Lambda Functions](../lambda/#id-3-toc-title): to execute custom code in response to events.

## Creating S3 Bucket Notifications

Automatically trigger SQS queues, SNS topics, or Lambda functions when specific events occur in your S3 bucket, for example, when a new object is created.

1. Navigate to **Cloud Services** -> **Storage**.
2. Select the **S3** tab.
3. In the **NAME** column, click the name of the bucket you want to configure.
4. Select the **Notifications** tab.
5.  Click **Add**. The **Add S3 Bucket Notification** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (672).png" alt=""><figcaption><p><strong>Add S3 Bucket Notification</strong> pane</p></figcaption></figure></div>
6. Complete the following fields:

<table data-header-hidden><thead><tr><th width="206.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Destination Type</strong></td><td>Select the service that will receive event notifications, e.g., <strong>SQS, SNS</strong>, or <strong>Lambda</strong>.</td></tr><tr><td><strong>Destination</strong></td><td>Select the specific destination resource (the SNS, SQS, or Lambda).</td></tr><tr><td><strong>Event Types</strong></td><td>Specify the events that will trigger notifications. You can select multiple events, e.g., <strong>All object create events</strong>, <strong>PUT</strong>, <strong>Object Removed</strong>.</td></tr></tbody></table>

8. Click **Save** to create the notification.

{% hint style="info" %}
**Tip:** A common use case is sending `All object create events` to an SQS queue to trigger downstream processing like Lambda or container services.
{% endhint %}

## Enabling Amazon EventBridge Notifications

In addition to specific event notifications, you can forward all S3 bucket events to Amazon EventBridge.

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Storage**.
2. Select the **S3** tab.
3. In the **NAME** column, click the name of the bucket you want to configure.
4. Select the **Notifications** tab.
5.  In the **Amazon EventBridge** section, click **Edit**. The **Edit Amazon EventBridge** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (671).png" alt=""><figcaption><p><strong>Edit Amazon EventBridge</strong> pane</p></figcaption></figure></div>
6. Select **On** or **Off** in the **Send notifications to Amazon EventBridge for all events in this bucket** list box.
7. Click **Save**.

{% hint style="info" %}
**Note:** EventBridge notifications are broad and include all supported bucket-level events. This is useful for centralized event routing or integrations with other AWS services via EventBridge rules.
{% endhint %}
