---
description: Create regional or global SSL certificates for GCP using Certificate Manager
---

# Managed SSL Certificates with Certificate Manager (Optional)

DuploCloud supports both **Compute Engine SSL certificates** and **GCP Certificate Manager certificates** (via certificate maps). While both are valid, we recommend **Certificate Manager** for most use cases. Certificate Manager certificates can be **created and validated independently of load balancers**, which improves automation support, allows reuse across services, and helps reduce the risk of downtime during load balancer creation. In contrast, Compute Engine certificates must be validated during load balancer setup, which can lead to delays or interruptions.

{% hint style="info" %}
If you followed the step [Certificate for Load Balancer](certificate-for-load-balancer-and-ingress.md), skip this step.
{% endhint %}

## Prerequisites&#x20;

* Obtain public and private certificate files from your chosen SSL certificate provider, such as GoDaddy or Namecheap.  Alternatively, you can create Google-managed certificates directly in Certificate Manager without uploading your own files.

## Creating a Certificate Map With Certificate Manager

To create a standalone SSL certificate with Certificate Manager, complete the following steps in Google Cloud CLI:

1. Create a DNS authorization resource using the following command where **YOUR\_DOMAIN** is your domain URL and **MAP\_NAME** is your certificate name (a unique name you choose for your certificate map).&#x20;

```
gcloud certificate-manager dns-authorizations create MAP_NAME \
  --domain="YOUR_DOMAIN"
gcloud certificate-manager dns-authorizations list
```

2. Manually create the DNS records shown in the output of the `list` command. You'll usually do this in the certificate's domain zone in the Cloud DNS service for the same project, but it depends on how you set up DNS.&#x20;
3. Create the certificate:

```
gcloud certificate-manager certificates create MAP_NAME \
  --domains="YOUR_DOMAIN,*.YOUR_DOMAIN" \
  --dns-authorizations=MAP_NAME
```

4. Create the certificate map and its entries:

```
gcloud certificate-manager maps create MAP_NAME
gcloud certificate-manager maps entries create MAP_NAME \
  --map="MAP_NAME" \
  --certificates="MAP_NAME" \
  --hostname="YOUR_DOMAIN"
gcloud certificate-manager maps entries create MAP_NAME-wildcard \
  --map="MAP_NAME" \
  --certificates="MAP_NAME" \
  --hostname="*.YOUR_DOMAIN"
```

5.  After your certificate map is created, register it in DuploCloud so it can be attached to services and load balancers: Navigate to **Administrator** -> **Plans**. Select the **Certificates** tab and click **Add**. The **Add a Certificate** pane displays. <br>

    <div align="left"><figure><img src="../../../.gitbook/assets/add cert image.png" alt="" width="365"><figcaption><p><strong>Add a Certificate</strong> pane</p></figcaption></figure></div>
6. Complete the following fields.

<table data-header-hidden><thead><tr><th width="198.22222900390625">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Enter a friendly display name used within DuploCloud only.</td></tr><tr><td><strong>GCP Certificate Type</strong></td><td>Select the certificate type used during creation. This must match what you created in GCP.</td></tr><tr><td><strong>GCP Certificate Map</strong></td><td>Enter the name of the certificate map created using Certificate Manager.</td></tr></tbody></table>

&#x20;5\. Click **Create**. The certificate will be available for selection when configuring HTTPS Load Balancers.
