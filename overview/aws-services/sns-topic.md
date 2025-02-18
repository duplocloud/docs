---
description: Creating SNS Topics
---

# SNS Topic

A SNS Topic is a logical access point that acts as a communication channel. It lets you group multiple _endpoints_ (such as [AWS Lambda](lambda/), [Amazon SQS](sqs-queue.md), HTTP/S, or an email address).

## Creating a SNS Topic

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **App Integration**.
2. Click **Add**. The **Create a SNS Topic** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/sns new.png" alt="" width="411"><figcaption><p>The <strong>Create a SNS Topic</strong> pane</p></figcaption></figure></div>

3. In the **Name** field, enter the SNS Topic name.
   * If you plan to select **FIFO Mode**, your SNS topic must end with the `.fifo` suffix, for example `my-topic.fifo`, to indicate that it is a **FIFO (First-In, First-Out) Topic**. Without this suffix, the topic will be treated as a standard topic.
4. From the **Encryption Key** list box, select a key.
5. Optionally, select **FIFO Mode** and **Enable FIFO content based deduplication**.
   * **FIFO Mode**: Ensures that messages are processed in the exact order they are sent.
   * **Enable FIFO content-based deduplication**: Prevents duplicate messages from being delivered to the subscribers if the same message content is sent within a 5-minute window.
6. Click **Create**.

## Setting SNS Topic Alerts

SNS Topic Alerts provide a flexible and scalable means of sending notifications and alerts across different AWS services and external endpoints, allowing you to stay informed about important events and incidents happening in your AWS environment.

To set alerts for SNS Topics, [see this procedure](../use-cases/faults-and-alarms/sns-topic-alerts.md).

{% hint style="info" %}
SNS Topics are used in event processing in conjunction with DynamoDB and Lambda, among other services. See the [AWS DynamoDB Developer's Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) for information, permissions information, and examples.
{% endhint %}
