---
description: >-
  Establish secure access to the DuploCloud portal with regional or global SSL
  certificates for GCP
---

# \[Optional] Create Managed SSL Certificates for GCP

{% hint style="info" %}
If you have your own certificate and you followed the step [Certificate for Load Balancer](certificate-for-load-balancer-and-ingress.md) then you can skip this.
{% endhint %}

SSL certificates secure connections between clients and servers or Load Balancers by encrypting information sent over the network using Transport Layer Security (TLS). GCP users have two options to configure SSL certificates: **Compute Engine SSL certificates resource (compute engine certificates)** and **Certificate Manager (certificate maps)**. For more information, see the Google Cloud documentation about the different [ways to configure SSL certificates in GCP](https://cloud.google.com/load-balancing/docs/ssl-certificates#config-tech) and [when to use Certificate Manager](https://cloud.google.com/certificate-manager/docs/overview#when-to-use).&#x20;

Although DuploCloud supports both certificate configuration methods, we recommend avoiding using compute engine certificates, if possible. This is because compute engine certificates can't be validated until they're attached to a Load Balancer, which can make it hard to manage uptime. In contrast, certificate maps can be validated in advance, circumventing potential downtime.&#x20;

## Creating a certificate map using Certificate Manager

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

5. Add the certificate map in the DuploCloud Plan. Navigate to **Administrator** -> **Plans**. Select the **Certificates** tab and click **Add**. The **Add a Certificate** pane displays.&#x20;
6. In the **Name** field, create a name for the certificate (the name is arbitrary as it is only a display name to be used within DuploCloud).&#x20;
7. In the **GCP Certificate Type** list box, select the certificate type. The certificate type must match the certificate entered in the `gcloud certificate-manager maps entries create` command.&#x20;
8. In the **GCP Certificate Map** field, enter the name of your map (in this example, **MAP\_NAME**). Click **Create**.

<div align="left">

<figure><img src="../../.gitbook/assets/add cert image.png" alt=""><figcaption><p>The <strong>Add a Certificate</strong> pane</p></figcaption></figure>

</div>

Now you can use your certificate with your DuploCloud Services.
