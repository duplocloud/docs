---
description: Assign AWS Elastic IPs to public Network Load Balancers
---

# Using Allocated IPs with AWS Load Balancers

DuploCloud allows you to assign IP addresses from an AWS-allocated block to your public-facing Network Load Balancers (NLBs). This ensures that your external services have consistent, predictable IP addresses, which can be important for DNS records, firewall rules, or regulatory requirements.

{% hint style="info" %}
**Note:** This feature is supported for public NLBs created for Docker, ECS, Shared Load Balancers, and Kubernetes Services. Internal-only load balancers are not eligible.
{% endhint %}

## Adding Allocated IPs to Plan Metadata

Before you can assign allocated IPs to a load balancer, you must register the AWS Elastic IPs in your Plan Metadata. Follow these steps:

1. In the DuploCloud Portal, navigate to **Administrator** → **Plans**.
2. From the **NAME** column, select the plan you want to configure.
3. Select the **MetaData** tab.
4.  Click **Add**. The **Add MetaData** pane displays.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/Screenshot (881).png" alt="" width="401"><figcaption><p><strong>Add MetaData</strong> pane</p></figcaption></figure></div>
5. In the **MetaData Key** field, enter: `NLBEIPAllocationIds`.
6. In the **Value** field, enter the **AWS Elastic IP Allocation IDs** for the addresses you want to use, separated by semicolons (`;`). For example: `eipalloc-0123456789abcdef0;eipalloc-0fedcba9876543210;eipalloc-0a1b2c3d4e5f67890`.
   * To find your Allocation IDs, go to the **AWS Management Console** and click **Elastic IPs** in the left-hand navigation. Each Elastic IP’s **Allocation ID** is listed in the **Allocation ID** column.
7. Click **Create** to save the metadata.&#x20;

Once this metadata is added, you will be able to choose to use elastic IPs from this pool when creating eligible public NLBs.

<figure><img src="../../../../.gitbook/assets/image (10) (3).png" alt=""><figcaption><p>Plan <strong>Metadata</strong> tab with allocated IP metadata highlighted</p></figcaption></figure>

## Selecting Allocated IPs When Creating a Listener

After adding the Elastic IP Allocation IDs to your plan metadata, you can assign them to a Network Load Balancer listener.

1. Navigate to your public NLB in DuploCloud.
2. Click **Add Listener**. The **Add Load Balancer Listener** pane displays.
3.  Select the **Use Elastic IPs from pool** option.\


    <div align="left"><figure><img src="../../../../.gitbook/assets/image (11) (3).png" alt="" width="375"><figcaption><p><strong>Add Load Balancer Listener</strong> pane</p></figcaption></figure></div>
4. Configure the remaining fields, as required, for the listener.
5. Click **Create** to add the listener.
