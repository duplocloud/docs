---
description: Create Google Cloud Run services in DuploCloud
---

# Cloud Run Service

[Google Cloud Run](https://cloud.google.com/run?hl=en#build-apps-or-websites-quickly-on-a-fully-managed-platform) allows you to run containerized applications in a fully managed serverless environment. It automatically scales services up or down based on incoming requests, making it ideal for stateless, event-driven workloads. You can deploy Cloud Run from the DuploCloud Platform, by configuring container images, replicas, environment variables, traffic rules, and networking settings. This integration ensures your serverless applications remain secure, governed, and aligned with your infrastructure policies.

## **Prerequisites**

* **Prepare Container Image**: Ensure your containerized application is ready for deployment. You can build your container image using any compatible runtime (Node.js, Python, Go, etc.) and push it to a container registry, such as Google Container Registry or Artifact Registry.
* **Configure IAM Permissions**: Ensure the DuploCloud platform has sufficient IAM permissions in GCP to create and manage Cloud Run services. These are usually set during initial onboarding, but check with your administrator if you encounter access issues.
* **Configure DuploCloud-Managed VPC Connector (if needed)**: If your Cloud Run service needs to access private network resources—such as a Cloud SQL instance with private IP, internal APIs, or services hosted in a private VPC—you must configure a VPC connector. DuploCloud can provision and manage this VPC connector for you. During deployment, you can reference the VPC connector in the **Advanced Options** area of the **Add Cloud Run Service** pane.

## **Creating a GCP Cloud Run Service**

1. In the DuploCloud Portal, navigate to **Cloud Services** → **Cloud Run Service**.
2.  Click **Add**. The **Add Cloud Run Service - Basic Options** pane displays.\


    <figure><img src="../../../.gitbook/assets/Screenshot (369).png" alt=""><figcaption><p>The <strong>Add Cloud Run Service - Basic Options</strong> pane</p></figcaption></figure>
3. Complete the fields:

<table data-header-hidden><thead><tr><th width="171.33331298828125"></th><th></th></tr></thead><tbody><tr><td><strong>Service Name</strong></td><td>Provide a unique name, such as <code>hello-world-service</code>.</td></tr><tr><td><strong>Image</strong></td><td>Specify the container image (e.g., <code>us-docker.pkg.dev/cloudrun/container/hello</code>).</td></tr><tr><td><strong>Minimum Replicas</strong></td><td>Set the minimum number of instances for the service to scale to.</td></tr><tr><td><strong>Maximum Replicas</strong></td><td>Set the maximum number of instances the service can scale to.</td></tr><tr><td><strong>Session Affinity</strong></td><td>Optionally, select <strong>Yes</strong> or <strong>No</strong> to enable or disable session affinity. Selecting <strong>Yes</strong> ensures requests from the same user are routed to the same instance.</td></tr><tr><td><strong>Environment Variables</strong></td><td>Optionally, add environment variables, such as API keys or database URLs.</td></tr><tr><td><strong>Labels</strong></td><td>Optionally, add labels to categorize or organize your service. For example: <code>env: production</code>.</td></tr><tr><td>A<strong>nnotations</strong><br></td><td>Optionally, add annotations for additional metadata.</td></tr></tbody></table>

4.  Click **Next**. The **Add Cloud Run Service - Advanced Options** pane displays.\


    <figure><img src="../../../.gitbook/assets/Screenshot (370).png" alt=""><figcaption><p>The <strong>Add Cloud Run Service - Advanced Options</strong> pane</p></figcaption></figure>
5. Optionally, update the **Advanced Options** fields:

<table data-header-hidden><thead><tr><th width="178.4444580078125"></th><th></th></tr></thead><tbody><tr><td><strong>Traffic</strong></td><td>Specify how traffic is routed to the service (e.g., 100% of traffic to the latest version), if needed.</td></tr><tr><td><strong>Ports</strong></td><td><p>Configure the container ports for the service, if needed. Example: </p><ul><li>Name: <code>http1</code></li></ul><ul><li>Container Port: <code>8080</code></li></ul></td></tr><tr><td><strong>Other Specs</strong></td><td>Define additional service specifications, if needed.</td></tr></tbody></table>

7. Click **Create** to deploy your Cloud Run service. Cloud Run will automatically scale the service based on incoming traffic.

## Managing Cloud Run Services

After you've deployed a Cloud Run service, you can view logs, edit configurations, and access the underlying GCP resource directly from the DuploCloud Portal.

1. Select the appropriate Tenant in the **Tenant** list box.
2. In the DuploCloud Portal, navigate to **Cloud Services** → **Cloud Run Service**.
3. Click on the menu icon (<img src="../../../.gitbook/assets/menu icon (8).avif" alt="" data-size="line">) in the row of the Cloud Run service you want to manage.
4. Select one of the following actions:

<table data-header-hidden><thead><tr><th width="193.5555419921875">Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>Logs</strong></td><td>Opens a live log view of your Cloud Run service's stdout/stderr output.</td></tr><tr><td><strong>View</strong></td><td>Displays the current configuration of the service in read-only mode.</td></tr><tr><td><strong>Edit</strong></td><td>Allows you to update the container image, environment variables, resources, and other settings.</td></tr><tr><td><strong>GCP Console</strong></td><td>Opens the service directly in the Google Cloud Console. Useful for debugging or advanced configuration.</td></tr><tr><td><strong>Delete</strong></td><td>Removes the Cloud Run service from DuploCloud and GCP. This action is irreversible.</td></tr></tbody></table>
