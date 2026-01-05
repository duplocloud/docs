---
description: Creating and Managing a Web Application Firewall (WAF)
---

# Web App Firewall (WAF)

DuploCloud allows you to integrate Web Application Firewalls (WAFs) to enhance the security of your applications. To get started, create the WAF in your cloud provider’s console. Once it's available, you can attach it to public-facing load balancers (ALBs) in the DuploCloud Portal to help protect your applications against common web threats such as SQL injection and cross-site scripting (XSS).

## Creating a Web Application Firewall (WAF)

When you create a WAF in DuploCloud, it is added to the Web ACL list for the selected Plan. You can then attach the WAF to specific load balancers as needed.\
\
Additionally, you have the option to set a WAF as the default for the Plan. When this option is selected, DuploCloud will automatically attach the WAF to all newly created public-facing load balancers, such as AWS Application Load Balancers (ALBs) or Azure Shared Application Gateways, providing consistent, automated protection across your infrastructure.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Plans**.&#x20;
2. From the **NAME** column, select the Plan you want to update.
3. Click the **WAF** tab.
4.  Click **Add**. The **Add WAF** pane displays.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (397).png" alt=""><figcaption><p>The <strong>Add WAF</strong> pane</p></figcaption></figure></div>
5. Complete the following fields.

<table data-header-hidden><thead><tr><th width="199.77777099609375"></th><th></th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Type a friendly name for your WAF to identify it within DuploCloud.</td></tr><tr><td><strong>WAF ARN</strong></td><td>Enter the full Amazon Resource Name (ARN) for AWS, or the equivalent resource ID for Azure.</td></tr><tr><td><strong>WAF Dashboard URL</strong></td><td>For AWS environments only, enter the URL to the WAF dashboard for monitoring and analytics. This is not required in Azure.</td></tr><tr><td><strong>Set as Default WAF</strong></td><td>Optionally, select this option to make this WAF the default for all new public-facing load balancers created in this Plan.</td></tr></tbody></table>

6. Click **Create**.

## Setting a Default WAF in a Plan

When [adding a WAF to a Plan](web-application-firewall-waf.md#creating-a-web-application-firewall-waf), you can make it the default by selecting the **Set as Default WAF** checkbox in the **Add WAF** pane. DuploCloud automatically attaches the default WAF to all new public-facing load balancers created in that Plan, including AWS Application Load Balancers (ALBs) and Azure Shared Application Gateways.

{% hint style="info" %}
**Note:**

* The default WAF applies only to load balancers created **after** the default is set; existing load balancers are unaffected.
* It attaches only to **public-facing** load balancers, not internal or private ones.
{% endhint %}

## Attaching a WAF to a Load Balancer

{% hint style="warning" %}
Only ALB Load Balancers can be attached to a WAF.
{% endhint %}

1. If you don't yet have an Application Load Balancer (ALB), [create one](../automation-platform/overview/aws-services/load-balancers/#adding-a-load-balancer).
2.  In the **Other Settings** card, click **Edit**. The **Other Load Balancer Settings** pane displays.<br>

    <div align="left"><figure><img src="../.gitbook/assets/Screenshot (273) (1).png" alt="" width="407"><figcaption><p>The <strong>Other Load Balancer Settings</strong> pane</p></figcaption></figure></div>
3. From the **Web ACL** list box, select a [WAF that you have added to DuploCloud](web-application-firewall-waf.md#creating-a-web-application-firewall-waf).&#x20;
4. Complete the other required fields in the **Other Load Balancer Settings** pane.
5. Click **Update**.

## Analyzing inbound traffic with the WAF dashboard <a href="#id-1-toc-title" id="id-1-toc-title"></a>

DuploCloud also provides a WAF Dashboard through which you can analyze the traffic that is coming in and the requests that are blocked. The Dashboard can be accessed from the left navigation panel: **Observability** -> **WAF**.

![WAF Dashboard](<../.gitbook/assets/waf (1).png>)
