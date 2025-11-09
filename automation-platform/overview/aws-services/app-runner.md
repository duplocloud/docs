---
description: Configure AWS App Runner services in DuploCloud
---

# App Runner

[AWS App Runner](https://docs.aws.amazon.com/apprunner/) is a fully managed service for running containerized web applications and APIs without managing infrastructure. It automatically handles container orchestration, load balancing, scaling, and secure traffic routing.

## Creating an App Runner Service

1. In the DuploCloud Portal, navigate to **Cloud Services** → **App Runner**.
2.  Click **Add**. The **Add App Runner Service** pane displays.\


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (873).png" alt=""><figcaption><p><strong>Create App Runner Service</strong> pane</p></figcaption></figure></div>
3. Complete the fields on the **Basic Options** pane:

<table data-header-hidden><thead><tr><th width="205.77777099609375">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Service Name</strong></td><td>Enter a unique name for the App Runner service.</td></tr><tr><td><strong>Image Repository Type</strong></td><td>Select the type of image repository. Choose <strong>ECR</strong> for a private registry or <strong>ECR_PUBLIC</strong> for a public registry.</td></tr><tr><td><strong>Image Identifier</strong></td><td>Enter the full URI of the container image.</td></tr><tr><td><strong>Port</strong></td><td>Enter the port your application listens on inside the container (e.g., <code>8080</code>).</td></tr><tr><td><strong>CPU</strong></td><td>Select the amount of CPU to allocate for the service from the available options (e.g., <strong>0.25 vCPU</strong>, <strong>0.5 vCPU</strong>).</td></tr><tr><td><strong>Memory</strong></td><td>Select the amount of memory to allocate for the service. For example, <strong>0.5 GB</strong> or <strong>1  GB</strong>.</td></tr><tr><td><strong>Auto Deployments Enabled</strong></td><td>Select this option to enable automatic deployments when the source image changes.</td></tr><tr><td><strong>Observability Enabled</strong></td><td><p>Select this option to enable logging and metrics collection via CloudWatch.</p><ul><li>When enabled, enter the ARN in the <strong>Observability Configuration ARN</strong> field.</li></ul></td></tr><tr><td><strong>Environment Variables</strong></td><td>Enter key-value pairs to set environment variables for the service.</td></tr><tr><td><strong>Environment Secrets</strong></td><td>Enter key-value pairs for sensitive data. Secrets are securely stored and injected into the service environment.</td></tr><tr><td><strong>Tags</strong></td><td>Enter key-value pairs to tag the service for identification, organization, or billing purposes.</td></tr></tbody></table>

4. Click **Next**. The **Advanced Options** pane displays.&#x20;
5. Complete the following configurations, if needed:&#x20;

<table data-header-hidden><thead><tr><th width="183.55548095703125">Section</th><th>Action / Description</th></tr></thead><tbody><tr><td><strong>Auto Scaling</strong></td><td>Enter the <strong>Auto Scaling Configuration ARN</strong> if using a custom configuration.</td></tr><tr><td><strong>Encryption</strong></td><td>If using KMS, select a <strong>KMS key</strong> to enable server-side encryption.</td></tr><tr><td><strong>Network</strong></td><td><p>Configure network options:</p><ul><li><strong>IP Address Type:</strong> Select the type of IP addresses for the service. Choose <strong>IPv4</strong> or <strong>Dual-stack</strong>.</li><li><p><strong>Outgoing Network Traffic:</strong> Select <strong>Public</strong> or <strong>VPC</strong>.</p><ul><li>If <strong>Public</strong> is selected, the service can access the internet directly.</li><li>If <strong>VPC</strong> is selected, the service can only access resources within the VPC. Enter the <strong>VPC Connector ARN</strong> when using <strong>VPC</strong>.</li></ul></li><li><strong>Incoming Network Traffic:</strong> Enable to make the service publicly accessible over the internet. Disable to restrict access to the VPC.</li></ul></td></tr><tr><td><strong>Health Check</strong></td><td><p>Configure health check settings:</p><ul><li><strong>Protocol:</strong> Specify the protocol to use for health checks (e.g., <strong>HTTP</strong> or <strong>TCP</strong>).</li><li><strong>Path:</strong> Enter the endpoint path to check for service health.</li><li><strong>Interval:</strong> Set the time between health checks.</li><li><strong>Timeout:</strong> Specify how long to wait for a response before marking the check as failed.</li><li><strong>Healthy Threshold:</strong> Enter the number of consecutive successful checks required to consider the service healthy.</li><li><strong>Unhealthy Threshold:</strong> Enter the number of consecutive failed checks required to consider the service unhealthy.</li></ul></td></tr></tbody></table>

5. Click **Create**. DuploCloud provisions the App Runner service and configures AWS resources automatically.

## Viewing App Runner Services

You can view details for any App Runner service in the DuploCloud Portal, including runtime information, deployment history, configuration, and endpoints.

1. In the DuploCloud Portal, go to **Cloud Services** → **App Runner** → **Services**.
2.  Click the name of the App Runner service you want to view details for.\


    <figure><img src="../../../.gitbook/assets/Screenshot (874).png" alt=""><figcaption><p><strong>Details</strong> tab for the App Runner service</p></figcaption></figure>
3. Use the tabs to explore service details:
   *   **Details**: displays the full service configuration in JSON format.

       Includes general info, image, instance, health check, network, auto scaling, and observability settings.
   * **YAML**: Displays the service configuration in YAML format.

{% hint style="info" %}
**Note:** The service endpoint is shown as the **URL** on the **Details** tab under the General section. Use this URL to access your running application.
{% endhint %}
