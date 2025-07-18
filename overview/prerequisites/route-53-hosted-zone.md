---
description: Create a Route 53 Hosted Zone to program DNS entries
---

# Route 53 Hosted Zone

To enable automatic DNS record creation in AWS, the DuploCloud Platform requires a unique Route 53 hosted zone. This hosted zone must be created outside of DuploCloud and configured as a DNS suffix in your infrastructure Plans. The domain should be a dedicated subdomain, such as `apps.[MY-COMPANY].com`.

{% hint style="danger" %}
**Important:** Never use this subdomain for any other purpose. DuploCloud takes ownership of all CNAME records within the domain and will remove any entries it does not manage.
{% endhint %}

For more details on how DNS works in DuploCloud and how to set up custom DNS names, see the [DNS Configuration documentation](../../duplocloud-prerequisites/resolving-dns-failures.md).&#x20;

## Creating a Route 53 Hosted Zone Using AWS Console

To enable DuploCloud to manage DNS records automatically, you need to create a dedicated Route 53 Hosted Zone in your AWS account.

1. Log in to [AWS Console](https://aws.amazon.com/console/).
2. Navigate to **Route 53 and Hosted Zones**.&#x20;
3. Create a new Route53 Hosted Zone with the desired domain name, for example, `apps.acme.com`.&#x20;
4. Access the Hosted Zone and note the [name server](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_Nameserver.html) names.
5. Go to your root domain’s DNS provider (for example, the registrar managing `acme.com`) and create an **NS record** for your subdomain (e.g., `apps.acme.com`). This NS record should point to the name servers assigned to your Route 53 Hosted Zone (the ones you noted earlier). This delegation ensures that DNS queries for your subdomain are routed to AWS Route 53 for resolution.

Once delegation is complete, provision the Route 53 Hosted Zone in each DuploCloud Plan—starting with the **DEFAULT** Plan, as described in the following section.

## Configuring DNS for a Plan

Configure a DuploCloud Plan to support automatic DNS record creation using AWS Route 53.\
Start by updating the **DEFAULT** Plan, then repeat the configuration for any additional Plans where DNS-managed Services or Ingresses will be deployed. DNS settings are not shared across Plans.

1. In the DuploCloud Portal, navigate to **Administrator** → **Plans**.
2. Click the name of the Plan from the **NAME** column (e.g., **DEFAULT**).
3. Select the **DNS** tab.
4. Click **Edit**. The **Set Plan DNS** pane displays.
5. Complete the following fields:

<table data-header-hidden><thead><tr><th width="213.99993896484375">Field</th><th>Description</th></tr></thead><tbody><tr><td><strong>Route53 Zone ID</strong></td><td>Enter the Hosted Zone ID from AWS Route 53. This is required to enable DNS support.</td></tr><tr><td><strong>External DNS Suffix</strong></td><td>Enter the DNS suffix for public-facing records (e.g., <code>.apps.acme.com</code>). Must begin with a dot (<code>.</code>).</td></tr><tr><td><strong>Internal DNS Suffix</strong></td><td>Enter the DNS suffix for internal resources (e.g., <code>.internal.acme.com</code>). Must begin with a dot (<code>.</code>).</td></tr><tr><td><strong>Ignore Global DNS</strong></td><td>Optionally, select this option to disable global DNS record management for the Plan, allowing localized DNS control.</td></tr></tbody></table>

6.  Click **Save** to apply your changes.\


    <figure><img src="../../.gitbook/assets/Screenshot (167).png" alt=""><figcaption><p><strong>DNS</strong> tab for the <strong>DEFAULT</strong> Plan</p></figcaption></figure>

{% hint style="warning" %}
Both the **External** and **Internal DNS Suffix** values must begin with a **dot (`.`)**.\
For example: `.apps.acme.com`. DNS entries will not be created correctly without the leading dot.
{% endhint %}
