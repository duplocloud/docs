---
description: Add custom tags to AWS resources
---

# Custom Resource tags

An Administrator can provide a list of custom tag names that can be applied to AWS resources for any Tenant in a DuploCloud environment.&#x20;

1. In the DuploCloud portal, navigate to **Administrator** -> **System Settings** -> **System Config**.&#x20;
2. Click **Add**. The **Add Config** pane displays.
3. In the **Config Type** list box, select **App Config**.
4. In the **Key** list box, select **Duplo Managed Tag Keys**.
5.  In the **Value** field, enter the name of the custom tag, for example, **cost-center**.<br>

    <div align="left"><figure><img src="../../../.gitbook/assets/image (14).png" alt="" width="381"><figcaption><p>Custom Tag- AppConfig with Key and Value</p></figcaption></figure></div>


6.  Click **Submit**. In the **System Configs** area of the **System Config** tab, your custom tag name is displayed with **Type AppConfig** and a **Key** value of **DUPLO\_CUSTOM\_TAGS**, as in the example below. <br>

    <figure><img src="../../../.gitbook/assets/Screenshot (199).png" alt=""><figcaption><p>Custom tag <strong>cost-center</strong> added to <strong>System Configs</strong></p></figcaption></figure>
7. Once the custom tag is added, navigate to **Administrator** -> **Tenants**.&#x20;
8. Select a Tenant from the **Name** column.&#x20;
9. Select the **Tags** tab and click **Add**.
10. In the **Key** field, enter the name of the custom tag (**cost-center** in the example) that you added to **System Config**.
11. In the **Value** field, enter an appropriate value. In the **Tags** tab, the tag **Key** and **Value** that you set are displayed, as in the example below.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (200).png" alt=""><figcaption><p>The <strong>cost-center</strong> tag with <strong>Value</strong> of <strong>engineering</strong></p></figcaption></figure>
