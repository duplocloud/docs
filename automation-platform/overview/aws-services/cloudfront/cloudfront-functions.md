---
description: Configure CloudFront Functions in DuploCloud
---

# CloudFront Functions

CloudFront Functions enable you to run lightweight JavaScript code at AWS edge locations to customize viewer requests and responses with low latency and high performance.

## Adding a CloudFront Function

1. In the DuploCloud Portal, navigate to **Cloud Services** -> **Networking**.
2. Select the **CloudFront** tab.
3. Select the **Functions** tab.
4.  Click **Add**. The **Add Function** page displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (684).png" alt=""><figcaption><p><strong>Add Function</strong> page</p></figcaption></figure></div>
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="230">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a unique name for the CloudFront function.</td></tr><tr><td><strong>Description</strong></td><td>Provide a short description of what the function does.</td></tr><tr><td><strong>Runtime Version</strong></td><td>Select the runtime version to use, e.g., <strong>cloudfront-js-2.0</strong>.</td></tr><tr><td><strong>Function Code</strong></td><td>Enter the JavaScript code for your function in the editor.</td></tr></tbody></table>

6. Click **Submit** to create the CloudFront Function.

Once created, you can associate this function with [CloudFront distributions](cloudfront.md) to customize behavior at the edge.
