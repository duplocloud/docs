---
description: Creating Google Cloud Scheduler jobs in DuploCloud
---

# Cloud Scheduler

[Google Cloud Scheduler](https://cloud.google.com/scheduler/docs/) is a fully managed cron job service. It allows you to run jobs (tasks) on a scheduled basis.&#x20;

## Creating Cloud Scheduler Jobs

You can set up recurring tasks that trigger **HTTP endpoints**, **Pub/Sub topics**, or **App Engine services** at specific intervals:

* **Pub/Sub**: Sends messages to a Pub/Sub topic. Commonly used for event-driven architectures.
* **App Engine**: Triggers an HTTP request to a specific App Engine service and version. Useful for Background tasks and scheduled jobs.
* **HTTP**: Sends HTTP requests to an endpoint (e.g., API or webhook) using methods like GET or POST.

### **Creating a Cloud Scheduler Job for Pub/Sub**

Before creating the Cloud Scheduler job, ensure that you have created a [Pub/Sub topic](s3-bucket-3.md), as the job will send messages to that topic.&#x20;

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Cloud Scheduler**.
2.  Click **Add**. The **Create Scheduler Job** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (275).png" alt=""><figcaption><p>The <strong>Create Scheduler Job</strong> pane</p></figcaption></figure>
3. Configure the Job settings:
   * **Name**: Provide a unique name for the job.
   * **Schedule**: Set the cron schedule (e.g., `0 12 * * *` for noon every day).
   * **Description**: Optionally, provide a description for the job.
   * **Time zone**: Select the desired time zone (default is UTC).
   * **Target Type**: Choose **Pub/Sub**.
     * **Topic Name**: Select the Pub/Sub topic to which messages will be published.
     * **Attributes**: Optionally, add custom attributes for the message.
     * **Data:** Optionally, enter the message body.&#x20;
4.  Click **Create**. The job will trigger based on the schedule you set, sending messages to the selected Pub/Sub topic.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (277) (1).png" alt=""><figcaption><p>The <strong>Cloud Scheduler</strong> page in the DuploCloud Portal</p></figcaption></figure>

After creating the Cloud Scheduler job, you can create a [Cloud Function](cloud-functions.md#creating-a-gcp-cloud-functions) that is subscribed to the Pub/Sub topic. The Cloud Function will automatically trigger when it receives a message from the Cloud Scheduler job, allowing you to automate tasks such as processing data or generating reports based on the message content.

### **Creating a Cloud Scheduler Job for App Engine**

Before creating the Cloud Scheduler job, ensure that you have already deployed a [Google App Engine](https://cloud.google.com/appengine?hl=en) application with the relevant endpoint (e.g., `/process-data`) that you want to trigger. The Cloud Scheduler job will send an HTTP request to this endpoint at the scheduled time.

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Cloud Scheduler**.
2.  Click **Add**. The **Create Scheduler Job** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (279).png" alt=""><figcaption><p>The <strong>Create Scheduler Job</strong> pane </p></figcaption></figure>
3. Configure the Job settings:
   * **Name**: Provide a unique name for the job.
   * **Schedule**: Set the cron schedule (e.g., `0 0 * * 0` for midnight every day).
   * **Description**: Optionally, provide a description for the job.
   * **Time zone**: Select the desired time zone (default is UTC).
   * **Target Type**: Choose **App Engine**.
     * **Service**: Enter the **App Engine service** to be invoked.
     * **Version**: Select the **version** of the service to use.
     * **HTTP Method**: Choose the HTTP method (e.g., GET, POST).
     * **Relative URI**: Optionally, enter the relative URI for the request (e.g., `/api/endpoint`).
     * **HTTP Body**: Optionally, enter the message body.
     * **HTTP Headers**: Optionally, add any necessary HTTP headers for the request.
4. Click **Create**. The job will trigger the specified App Engine service based on the cron schedule.

<figure><img src="../../../.gitbook/assets/Screenshot (280).png" alt=""><figcaption><p>The <strong>Cloud Scheduler</strong> page in the DuploCloud Portal</p></figcaption></figure>

### **Creating a Cloud Scheduler Job for HTTP**

Before creating the Cloud Scheduler job, ensure that you have already deployed either an HTTP-based service or a [Cloud Function](cloud-functions.md#creating-a-gcp-cloud-functions) with the relevant endpoint (e.g., `/process-orders`) that you want to trigger. The Cloud Scheduler job will send an HTTP request to this endpoint or invoke the Cloud Function at the scheduled time.

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Cloud Scheduler**.
2.  Click **Add**. The **Create Scheduler Job** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (282).png" alt=""><figcaption><p>The <strong>Create Scheduler Job</strong> pane</p></figcaption></figure>
3. Configure the Job settings:
   * **Name**: Provide a unique name for the job.
   * **Schedule**: Set the cron schedule (e.g., `0 12 * * *` for noon every day).
   * **Description**: Optionally, provide a description for the job.
   * **Timezone**: Select the desired time zone (default is UTC).
   * **Target Type**: Choose **HTTP**.
     * **HTTP Method**: Choose the HTTP method (e.g., GET, POST).
     * **Cloud Function**: If you have an existing Cloud Function that can be triggered by HTTP, select it here. If you do not have any Cloud Functions deployed, the dropdown will show **Other** as the only option.
     * **Target URI**: Enter the full URL of the target HTTP endpoint (e.g., `https://example.com/api`).
     * **Authentication Method**: Choose the authentication method required for the target service (e.g., **oauth token**, **oidc token**, etc.).
     * **HTTP Body**: Optionally, enter the body of the HTTP request (e.g., `{ "order_id": 12345 }` for a POST request).
     * **HTTP Headers:** Optionally, add any necessary HTTP headers for the request.
4.  Click **Create**. The job will make an HTTP request to the specified endpoint according to the cron schedule.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (283).png" alt=""><figcaption><p>The <strong>Cloud Scheduler</strong> page in the DuploCloud Portal</p></figcaption></figure>

