---
description: Manage custom tags for AWS resources in DuploCloud
---

# Custom Resource Tags

DuploCloud provides flexible tagging capabilities to help you organize and manage your AWS resources.

There are two primary ways to apply custom tags:

* **Tenant-wide tags**: Configured centrally by administrators and applied to all resources within a tenant, ensuring consistent metadata across your environment.
* **Resource-specific tags**: Added manually on individual resources, allowing you to customize tags for specific resource needs.

## Configuring Tenant-Wide Custom Resource Tags

An administrator can define a list of custom tag keys that are allowed to be applied to AWS resources for any tenant in a DuploCloud environment. After defining these keys, specific tag values can be assigned to each tenant to apply the tags automatically across all resources within that tenant.

### Defining allowed tenant-wide tag keys

Define the custom tag keys that can be assigned tenant-wide.

1. In the DuploCloud portal, navigate to **Administrator** -> **System Settings** -> **System Config**.&#x20;
2.  Click **Add**. The **Add Config** pane displays.<br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (850).png" alt=""><figcaption><p><strong>Add Config</strong> pane</p></figcaption></figure></div>
3. In the **Config Type** list box, select **App Config**.
4. In the **Key** list box, select **Duplo Managed Tag Keys**.
5. In the **Value** field, enter one or more Duplo tag keys, separated by semicolons. For example: `Cost-Center; Company; Cost`.
6.  Click **Submit**. The tag key will appear in the System Configs list as `DUPLO_CUSTOM_TAGS`, indicating it was successfully added.<br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (852).png" alt=""><figcaption><p><strong>System Configs</strong> list with <code>DUPLO_CUSTOM_TAGS</code> key highlighted</p></figcaption></figure></div>

### Assigning tag values to tenants

Assign specific values to the allowed tenant-wide tag keys for each tenant to apply these tags automatically to all resources managed under that tenant.

1. Navigate to **Administrator** -> **Tenants**.&#x20;
2. Click the Tenant name in the **NAME** column.&#x20;
3. Select the **Tags** tab.&#x20;
4.  Click **Add**. The **Add Tenant Tag** pane displays. <br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (851).png" alt=""><figcaption><p><strong>Add Tenant Tag</strong> pane</p></figcaption></figure></div>
5. Select one of the tenant-wide tag keys configured earlier (e.g., `Cost-Center`) in the **Key** list box.
6. Enter the appropriate value for this tenant in the **Value** field.
7. Click **Save**. The tag key and value will now be applied automatically to all AWS resources managed under this tenant.

<figure><img src="../../.gitbook/assets/Screenshot (853).png" alt=""><figcaption><p><strong>Tags</strong> tab showing the <code>cost-center</code> tag key and its assigned value</p></figcaption></figure>

## Configuring Resource-Specific Custom Tags

Beyond tenant-wide tags, DuploCloud allows you to add custom tags directly to individual AWS resources. This lets you apply specific metadata to resources for organization, tracking, or operational needs that vary by resource.

1. Navigate to the resource’s page in the DuploCloud Portal. For example, for an RDS, navigate to **Cloud Services** -> **Databases** -> **RDS**, and click the RDS name in the **NAME** column.
2. Select the **Tags** tab.
3.  Click **Add**. The **Add Resource** **Tag** pane displays. <br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (773).png" alt=""><figcaption><p><strong>Add Resource</strong> pane</p></figcaption></figure></div>
4. Enter the **Key** and **Value** for the custom tag.
5.  Click **Add**. The custom tag is added to the resource and displayed on the **Tags** tab.<br>

    <div align="left"><figure><img src="../../.gitbook/assets/Screenshot (774).png" alt=""><figcaption><p><strong>Tags</strong> tab for the RDS </p></figcaption></figure></div>

{% hint style="info" %}
**Note:** Custom tags added here apply only to the specific resource and do not affect other resources in the tenant. Tenant-wide tags configured by administrators are applied automatically and managed separately.
{% endhint %}

## Custom Tags Best Practices

* Avoid using the same tag keys for both tenant-wide and resource-specific tagging unless you want intentional overrides.
* Use tenant-wide tags for organization-wide or team-wide metadata (like `cost-center`, `environment`).
* Use resource-specific tags for granular control or temporary tagging (like `backup-window`, `owner`).
