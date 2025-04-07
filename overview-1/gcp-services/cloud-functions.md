---
description: Create Google Cloud Functions in DuploCloud
---

# Cloud Functions

Google Cloud Functions allow you to run serverless code that automatically scales based on incoming events. You can trigger Cloud Functions via HTTP requests, Cloud Storage events, Pub/Sub messages, and more. This makes them ideal for lightweight, scalable applications that need to react to real-time events.

## **Prerequisites**

**Preparing your code**: Ensure your code package (ZIP file) is ready for deployment. Google Cloud Functions support various programming languages, including Node.js, Python, Go, and more. You can write the function locally or use an existing code package.

**Uploading the Code to Cloud Storage:** Before deploying your Cloud Function, create a Cloud Storage bucket to store the code for your Cloud Function's deployment:

* [Create a Storage Bucket](s3-bucket-2.md#creating-a-gcp-cloud-storage-bucket) to hold your code package.
* In GCP Console, upload your code package (ZIP file) to the bucket:
  * Navigate to **Cloud Services** -> **Storage**.
  * In the row of the bucket you created, click on the menu icon (<img src="../../.gitbook/assets/menu icon (6).avif" alt="" data-size="line">) and select **GCP Console**.&#x20;
  * In GCP Console, upload your code package to the bucket.
  * After uploading, note the file path (location) of your code package in the bucket, as you will need this when configuring your Cloud Function. For example, `gs://my-cloud-function-bucket/my-function-code.zip` .

## Creating a GCP Cloud Function

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Functions**.
2.  Click **Add**. The **Create Function** pane displays.\


    <figure><img src="../../.gitbook/assets/Screenshot (285).png" alt=""><figcaption><p>The <strong>Create Function</strong> pane</p></figcaption></figure>
3. Configure the Function Settings:
   * **Name**: Provide a unique name for the cloud function. For example, `hello-world-function`.
   * **Description**: Provide an optional description of the function. This can be any text explaining the function's purpose.
   * **Runtime**: Select the runtime environment for your cloud function (e.g., Node.js, Python, etc.).
   * **Available Memory**: Specify the amount of memory allocated to the cloud function. For example, `256 MB`.
   * **Timeout (in seconds)**: Set the maximum allowed execution time for the cloud function. For example, `60` seconds.
   * **Entry Point**: Specify the entry point for the function. This is the method or function that gets called when the function is triggered. For example, `exports.handler` in Node.js.
   * **Trigger Type**: Select the type of trigger that will invoke the cloud function. For example, `HTTPS trigger`.
   * **Require HTTPS instead of HTTP**: Optionally, enable this setting to require secure HTTPS instead of HTTP for the trigger. This setting ensures the function is only triggered via HTTPS.
   * **Source Archive Bucket**: Specify the name of the storage bucket that contains your function's source code.
   * **Source Archive Path**: Enter the path in the source bucket where the code archive is located.
   * **Ingress Type**: Specify the type of ingress allowed for the cloud function. For example, `All` to allow all traffic or limit it to specific IPs or VPCs.
   * **VPC Routing**: Choose whether the function should have access to a Virtual Private Cloud (VPC). Select this option if the function needs to interact with private resources in a VPC.
   * **Environment Variables**: Provide any environment variables needed by your function. This could include API keys, database URLs, etc.
   * **Build Environment Variables**: Define any environment variables needed during the build phase of the function.
   * **Labels**: Optionally, add labels to categorize or organize your cloud function. For example, `env: production` or `service: hello-world`.
4. Click **Create**. The cloud function is created with the configurations you specified.\
