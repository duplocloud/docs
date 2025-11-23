---
description: Create and manage Google Cloud Task queues from the DuploCloud Portal
---

# GCP Cloud Task Support

[Google Cloud Tasks](https://cloud.google.com/tasks/docs) is a fully managed service that enables you to run asynchronous background work using task queues. Queues help offload work from your application, manage retries, and control task execution rates, improving system efficiency and resilience.

DuploCloud simplifies Google Cloud Tasks by allowing you to create and manage task queues and individual tasks directly from the Portal. This lets you easily incorporate background processing into your GCP workloads without writing scripts or configuring the service manually in Google Cloud.

## Creating a Cloud Task Queue

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Cloud Tasks**.
2. Select the **Queues** tab.
3.  Click **Add**. The **Create Queue** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (591).png" alt=""><figcaption><p><strong>Create Queue</strong> pane</p></figcaption></figure></div>
4. Provide a **Name** for the queue.
5. In the **Location** list box select the GCP region where the queue will be created (e.g., `us-central1`).
6.  Click **Create** to provision the queue in GCP. Once created, the queue appears in the list on the **Queues** tab.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (592).png" alt=""><figcaption><p><strong>Queues</strong> tab in the DuploCloud Portal</p></figcaption></figure>

## Managing Cloud Task Queues

To manage an existing queue:

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Cloud Tasks**.
2. Select the **Queues** tab.
3.  Click the menu icon (<img src="../../../.gitbook/assets/menu icon (16).avif" alt="" data-size="line">) in the row of the queue you want to manage.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (593).png" alt=""><figcaption><p><strong>Queues</strong> tab with menu options highlighted</p></figcaption></figure>
4. Choose one of the following actions:
   * **GCP Console**: opens the selected queue in the Google Cloud Console for advanced configuration and monitoring.
   * **Delete**: permanently removes the queue and any associated tasks from your GCP environment.

## Creating a Task in a Cloud Task Queue

Once a queue is created, you can add individual tasks:

1. In the DuploCloud Platform, navigate to **Cloud Services** -> **Cloud Tasks**.
2. Select the queue name from the **NAME** column.
3. Select the **Tasks** tab.
4.  Click **Add**. The **Create Task** pane displays.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (595).png" alt=""><figcaption><p><strong>Create Task</strong> pane</p></figcaption></figure></div>
5. Complete the required fields:&#x20;

<table data-header-hidden><thead><tr><th width="229.111083984375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the task. This field is required.</td></tr><tr><td><strong>Task Type</strong></td><td>Select the type of task, e.g., <strong>Http</strong> or <strong>AppEngine</strong>.</td></tr><tr><td><strong>URL</strong></td><td>Enter the full URL for the HTTP target. It must begin with <code>http://</code> or <code>https://</code>.</td></tr><tr><td><strong>HTTP Method</strong></td><td>Choose the HTTP method to use for the request, e.g., <strong>Post</strong>.</td></tr><tr><td><strong>Request Body</strong></td><td>Optionally, enter a payload to include in the request body. This is supported for most HTTP methods that allow a body, such as <code>POST</code>, <code>PUT</code>, and <code>PATCH</code>.</td></tr><tr><td><strong>Add a Header</strong></td><td>Optionally, select this option to include one or more custom HTTP headers. For each header, enter a <strong>Name</strong> and <strong>Value</strong>.</td></tr></tbody></table>

6.  Click **Submit** to create the task. Once created, the task appears in the list under the **Tasks** tab.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (596).png" alt=""><figcaption><p><strong>Tasks</strong> tab for a Cloud Task Queue in the DuploCloud Portal</p></figcaption></figure></div>

## Managing Tasks in a Queue

Once tasks have been created, you can manage them directly from the DuploCloud Portal:

1. Navigate to **Cloud Services** -> **Cloud Tasks**.
2. Click the name of the queue that contains the task you want to manage.
3. Select the **Tasks** tab.
4.  In the row of the task you want to manage, click the menu icon (<img src="../../../.gitbook/assets/menu icon (17).avif" alt="" data-size="line">).<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (597).png" alt=""><figcaption><p><strong>Tasks</strong> tab with menu options highlighted</p></figcaption></figure>
5. Choose one of the following actions:

<table data-header-hidden><thead><tr><th width="194.44439697265625">Option</th><th>Description</th></tr></thead><tbody><tr><td><strong>JSON</strong></td><td>View the full task definition in JSON format.</td></tr><tr><td><strong>Force Run</strong></td><td>Immediately execute the task, bypassing its scheduled run time.</td></tr><tr><td><strong>Delete</strong></td><td>Permanently remove the task from the queue.</td></tr></tbody></table>

### Additional Resources

* [Google Cloud Tasks Overview](https://cloud.google.com/tasks/docs)
* [Creating and Managing Queues](https://cloud.google.com/tasks/docs/creating-queues)
