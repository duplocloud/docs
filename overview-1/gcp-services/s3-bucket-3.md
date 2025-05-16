---
description: Create Pub/Sub Topic in GCP
---

# Pub/Sub

## Add a Pub/Sub topic

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Pub/Sub**.
2.  Select the **Topics** tab, and click **Add**. The **Create a PubSub Topic** pane displays.\


    <div align="left"><figure><img src="../../.gitbook/assets/topic pane (1).png" alt=""><figcaption><p>The <strong>Create a PubSub Topic</strong> pane</p></figcaption></figure></div>
3. Provide a **Name** for the Pub/Sub Topic.
4. Enter necessary labels in the **Labels** field, (e.g., `env: production`).
5. Click **Create**. The Pub/Sub topic is created.&#x20;

## Create a Pub/Sub Topic Subscription

1. From the DuploCloud Portal, navigate to **Cloud Services** -> **Pub/Sub**.
2. Select the **Subscriptions** tab, and click **Add**. The **Create Subscription** pane displays.

<figure><img src="../../.gitbook/assets/PubSub Subscription.png" alt=""><figcaption><p>The <strong>Create Subscription</strong> pane in the DuploCloud Portal</p></figcaption></figure>

3. Provide a **Name** for the subscription.
4. Select the Pub/Sub topic for reference from the **Topic** list box.&#x20;
5. From the **Delivery Type** list box, select one of these options:
   * **Pull**: Allows the subscriber to manually pull messages from the subscription at their own pace.
   * **Push**: Automatically pushes messages to a specified endpoint (e.g., HTTP server or API) as soon as they are published to the topic.
   * **BigQuery**: Delivers messages directly to a Google BigQuery table for analytics and data processing.
   * **Cloud Storage**: Sends messages to a specified Cloud Storage bucket, storing them as objects for later retrieval or processing.
6. Adjust the **Acknowledgement Deadline (seconds)**, if needed. This value is the maximum time after a subscriber receives a message before the subscriber should acknowledge the message.
7. Complete additional required fields depending on the **Delivery Type**:&#x20;
   * **Pull**
     * No additional fields required.&#x20;
   * **Push**&#x20;
     * **Endpoint**: Enter the URL to which the messages will be sent.
     * **Attributes** (Optional): Define any optional key-value attributes to be included in the push request.
   * **BigQuery**
     * **Table Name**: Specify the name of the BigQuery table where messages will be stored.
     * **Schema**: Select the schema for the table to structure the data appropriately.
     * Optionally enable **Write Metadata** or **Drop Unknown Fields**.
   * **Cloud Storage**
     * **Bucket**: Enter the name of the Cloud Storage bucket where the messages will be stored as objects.

<figure><img src="../../.gitbook/assets/creat sub completed.png" alt=""><figcaption><p>The filled <strong>Create Subscription</strong> pane</p></figcaption></figure>

8. Click **Create**. The subscription is displayed on the **Subscriptions** tab.

<figure><img src="../../.gitbook/assets/sub success.png" alt=""><figcaption><p>The <strong>Pub/Su</strong>b <strong>Subscriptions</strong> page in the DuploCloud Portal</p></figcaption></figure>

