---
description: Using Amazon SQS in DuploCloud
---

# SQS Queue

Amazon Simple Queue Service (Amazon SQS) offers a secure, durable, and available hosted queue to integrate and decouple distributed software systems and components. It provides a generic web service API that you can access using any programming language that AWS SDK supports.

The following Amazon SQS Queue types are supported.

* **Standard Queues** - Standard queues support a nearly unlimited number of API calls per second, per API action (`SendMessage`, `ReceiveMessage`, or `DeleteMessage`). Standard queues support at-least-once message delivery. However, occasionally (because of the highly distributed architecture that allows nearly unlimited throughput), more than one copy of a message might be delivered out of order. Standard queues provide best-effort ordering which ensures that messages are generally delivered in the same order as they're sent.
* **FIFO Queues** - FIFO queues have all the capabilities of a Standard queue, but are designed to enhance messaging between applications when the order of operations and events is critical, or where duplicates cannot be tolerated.

## Creating SQS queues

### Creating a standard SQS queue

1. in the DuploCloud portal, navigate to **Cloud Services** -> **App Integration**.
2. Click the **SQS** tab.
3.  Click **Add**. The **Create a SQS Queue** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/sqs stansard.png" alt="" width="341"><figcaption><p>The <strong>Create a SQS Queue</strong> pane</p></figcaption></figure></div>
4. Enter an SQS Queue **Name**.
5. Select **Standard** from the **Queue Type** list box.
6. Enter **Message Retention Period (in Seconds)**. For example, **345600** seconds in the example equates to four days.
7. Enter the **Visibility Timeout** in seconds. In the example, we specify **30** seconds.&#x20;
8. Optionally, select **Configure Dead Letter Queue**, select the **Target SQS dead letter queue**, and specify the number of **Message process attempts before dead letter queue**.&#x20;
9. Click **Create**.

### Creating a SQS FIFO queue

1. In the DuploCloud portal, navigate to **Cloud Services** -> **App Integration**.
2. Click the **SQS** tab.
3. Click **Add**. The **Create a SQS Queue** pane displays.

<div align="left"><figure><img src="../../.gitbook/assets/sqs fifo.png" alt="" width="342"><figcaption><p>The <strong>Create a SQS Queue</strong> pane</p></figcaption></figure></div>

4. Enter an SQS Queue **Name**.
5. Select **FIFO** from the **Queue Type** list box.
6. Enter **Message Retention Period (in Seconds)**. For example, **345600** seconds in the example below equates to four days.
7. Enter the **Visibility Timeout** in seconds. In the example below, we specify **30** seconds.
8. Optionally, select **Content-based deduplication**. Selecting this option indicates that message deduplication IDs are used to ensure duplicate messages are not sent. If a message deduplication ID is sent successfully, any messages sent with the same message ID aren't delivered within five minutes.
9. Select either **Queue** or **Message group** from the **Deduplication scope** list box:
   * **Queue:** Deduplication processing occurs at the Queue level. The **FIFO throughput limit** is automatically set to **Per queue**.
   * &#x20;**Message group:** Deduplication processing occurs at the [Message group ](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/using-messagegroupid-property.html)level, using Message group IDs. In the **FIFO throughput limit** list box, select **Per queue** or **Per message group ID** to specify whether the FIFO Throughput Quota applies to the entire **FIFO Queue** or individually to each **Message Group**.
10. Optionally, select **Configure Dead Letter Queue**, select the **Target SQS dead letter queue**, and specify the number of **Message process attempts before dead letter queue**.&#x20;
11. Click **Create**.

## Dead Letter Queue (DLQ) and redrive policy

You can configure a Dead Letter Queue (DLQ) and a redrive policy to manage messages that cannot be processed successfully. A DLQ stores failed messages, preventing them from blocking the normal operation of the queue. The redrive policy allows you to define how many times a message can be retried before it is moved to the DLQ. This feature enhances the reliability and manageability of your message processing system.

You can configure a Dead Letter Queue and redrive policy either when creating a new SQS or SQS FIFO queue or by editing an existing queue:

To **configure DLQ and redrive policy during queue creation**, follow the instructions above to create an [SQS queue](sqs-queue.md#creating-sqs-queues) or [SQS FIFO queue](sqs-queue.md#creating-fifo-queues). Select **Configure Dead Letter Queue**, select the **Target SQS dead letter queue**, and specify the number of **Message process attempts before dead letter queue**.

To **edit an existing queue** and configure the DLQ and redrive policy, use the procedure provided below.

### Configuring a DQL and redrive policy

1. Select the name of the Tenant that contains the SQS or SQS FIFO queue from the **Tenant** list box.&#x20;
2. Navigate to **Cloud Services** -> **App Integration**.
3. Select the **SQS** tab.
4. Select the name of the SQS or SQS FIFO queue from the **NAME** column.&#x20;
5. Click on the **Actions** menu, and select **Edit**. The **Edit SQS** **Queue** or **Edit** **SQS FIFO Queue** pane displays.&#x20;
6. Enable **Configure Dead Letter Queue**.&#x20;
7. Select the **Target SQS dead letter queue**.
8. Specify the number of **Message process attempts before dead letter queue**.&#x20;
9. Click **Update**. The DQL and redrive settings for the SQS or SQS FIFO queue are configured.&#x20;
