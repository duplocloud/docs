---
description: Managing custom DNS records in DuploCloud
---

# DNS Configuration

DuploCloud automatically creates and manages DNS records for many resources you deploy, such as Kubernetes Services or VM hosts with public IPs, by integrating with your cloud provider’s DNS service. These DNS records are essential for routing traffic to your workloads and Services.

In most cases, DNS names are created automatically and can be customized within the DuploCloud Platform. However, you may sometimes need to manually configure or troubleshoot DNS entries, such as when using custom domain names, ensuring DuploCloud doesn’t overwrite DNS records you manage outside of the platform, or resolving DNS failures.

## Prerequisites

* **Configure your DNS zones**: Make sure your DNS zones are properly configured in both DuploCloud and your cloud provider. This often involves setting up subdomain zones (like `apps.mycompany.com`) and connecting them to DuploCloud. See DNS setup instructions for your cloud provider:
  * AWS: [Configure Route 53 DNS Zones](../overview/prerequisites/route-53-hosted-zone.md)
  * GCP: [Configure Cloud DNS Zones](../overview-1/prerequisites/route-53-hosted-zone.md)
  * Azure: [Program DNS Entries](../overview-2/prerequisites/program-dns-entries.md)

## **Adding Custom DNS Names**

You can configure a custom DNS name for resource directly in the DuploCloud Platform, or manually in your cloud provider’s platform.&#x20;

### **Creating Custom DNS Names in DuploCloud**

For resources that DuploCloud manages (like services behind Load Balancers), you can customize the automatically generated DNS name:

1. In the **Tenant** list box, select the Tenant.
2. Navigate to the **Services** page (**Kubernetes** -> **Services**, or **Docker** -> **Services**). The **Services** page displays.
3. Select your Service from the **NAME** column.
4. Click the **Load Balancers** tab.&#x20;
5. In the **DNS Name** card, click **Edit**.&#x20;
6. The prefix in the DNS Name is editable. Select a meaningful DNS Name prefix.
7. Click **Save**. A success message briefly displays at the top center of the DuploCloud Portal. Your new DNS name is now registered.

### **Creating Custom DNS Names in Your Cloud Provider**

For resources that don’t have DNS configuration in DuploCloud (e.g., non-Kubernetes services), you will need to manually add DNS entries in your cloud provider’s DNS service.

* **For AWS**:[ Add custom DNS records in AWS Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-creating.html)
* **For GCP**: [Add custom DNS records in Google Cloud DNS](https://cloud.google.com/dns/docs/records/)
* **For Azure**: [Add custom DNS records in Azure DNS](https://learn.microsoft.com/en-us/azure/dns/dns-operations-recordsets-portal)

{% hint style="warning" %}
DuploCloud automatically deletes DNS records that it does not manage. If you create custom DNS names directly in your cloud provider, you must [configure DuploCloud to ignore unmanaged entries](resolving-dns-failures.md#configuring-duplocloud-to-ignore-dns-entries) so they aren’t automatically removed.
{% endhint %}

## Configuring DuploCloud to Ignore DNS Entries

If you create a DNS entry directly in your cloud provider’s platform (AWS, Google Cloud, or Azure), DuploCloud may delete it during updates, as it automatically deletes any DNS entries it did not create. To prevent this from happening, configure Systems Settings to ignore specific DNS entries.

1. From the DuploCloud Portal, navigate to **Administrator** -> **System Settings** -> **System Config**.
2.  Click **Add**. The **Add Config** pane displays. <br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (362).png" alt="" width="360"><figcaption><p>The <strong>Add Config</strong> pane</p></figcaption></figure></div>
3. Fill the fields:

<table data-header-hidden><thead><tr><th width="171.3333740234375"></th><th></th></tr></thead><tbody><tr><td><strong>Config Type</strong></td><td><code>AppConfig</code></td></tr><tr><td><strong>Key</strong></td><td><code>CNAME Prefixes to Ignore</code></td></tr><tr><td><strong>Value</strong></td><td>Enter the DNS prefixes to ignore. For example, entering <code>test</code> will prevent DuploCloud from deleting DNS entries like <code>test.apps.duplocloud.net</code>.</td></tr></tbody></table>

4. Click **Submit**. DuploCloud will ignore the specified DNS prefixes.&#x20;

## Resolving DNS Failures

Occasionally, DNS resolution can fail on local machines, especially for private resources behind VPNs. This is often caused by incorrect DNS server settings or local DNS caching.

To fix this:

* Use public DNS servers like `8.8.8.8` (Google) or `1.1.1.1` (Cloudflare).
* Flush your DNS cache.
* Verify VPN connection if accessing private resources.

