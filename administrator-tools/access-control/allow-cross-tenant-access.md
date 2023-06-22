---
description: Allow multiple Tenants access to the same resources
---

# Cross-Tenant Access

{% hint style="info" %}
These features are currently only available for AWS.
{% endhint %}

## Allowing Cross-Tenant access based on Security Groups

To allow access between two Tenants, based on Security Groups in the underlying Cloud Platform, perform this procedure using the Tenant **Security** tab. For services that are restricted by IAM policies, see [Cross-Tenant access to restricted policy-based resources](allow-cross-tenant-access.md#cross-tenant-access-to-restricted-policy-based-resources).

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenants**.
2. Select the Tenant whose resources you want to share from the **Name** column.
3. Click the **Security** tab.
4. Click **Add**. The **Add Tenant Security** pane displays.
5. From the **Source Type** list box, select **Tenant**.
6. From the **Tenants** list box, select another Tenant with which you want to share resources.
7. From the **Protocol** list box, select the protocol that you want to use for sharing.
8. In the **Port Range** field, specify the range of ports to which you want to grant access.
9. Add a user-friendly **Description** of this sharing rule.
10. Click **Add**.

<figure><img src="../../.gitbook/assets/Screen Shot 2023-03-07 at 6.09.09 PM.png" alt=""><figcaption><p><strong>Add Tenant Security</strong> pane</p></figcaption></figure>

## Cross-Tenant access to restricted policy-based resources

To allow access, or create a share, between two Tenants for services that are restricted by IAM policies, perform this procedure using the Tenant **Grants** tab. To establish general non-IAM restricted Cross-Tenant access, see [Allowing Cross-Tenant access to non-restricted services](allow-cross-tenant-access.md#allowing-cross-tenant-access-to-non-restricted-services).

{% hint style="info" %}
Ensure that the two Tenants that are sharing resources reside within the same region in the AWS Portal.
{% endhint %}

1. In the DuploCloud portal, navigate to **Administrator** -> **Tenants**. The **Tenants** page displays.
2. From the **Name** column, select the Tenant with access to the restricted resource that you want to share. In this example, we choose to share resources to which Tenant **uat-01** has access.
3.  Click the **Grants** tab. Select **Allow Other Tenants to access **_**TENANT\_NAME**_, where _**TENANT\_NAME**_ is the Tenant you selected.

    <figure><img src="../../.gitbook/assets/AWS_GCT_selector.png" alt=""><figcaption><p><strong>Grants</strong> tab with <strong>Allow Other Tenants to access </strong><em><strong>TENANT_NAME</strong></em> option </p></figcaption></figure>
4.  Click **Add**. The **Grant Cross-Tenant Access** pane displays.\


    <figure><img src="../../.gitbook/assets/G1.png" alt=""><figcaption><p><strong>Grant Cross-Tenant Access</strong> pane</p></figcaption></figure>


5. From the **Requesting Tenant** list box, select the Tenant with which you want to share access. In this example, the **Requesting Tenant** is **demo01**.
6. From the **Access to Area** list box, select the restricted policy-based resource that you want to share.
7. Click **Create**. Your Cross-Tenant Access share is created.

### Viewing Cross-Tenant grants to restricted policy-based resources

1. In the DuploCloud portal, navigate to **Administrator** -> **Tenants**. The **Tenants** page displays.
2. From the **Name** column, select the Tenant whose Cross-Tenant grants you want to view. In this example, we select Tenant **uat-01**.
3. Click the **Grants** tab. Select **Allow Other Tenants to access **_**TENANT\_NAME**_, where _**TENANT\_NAME**_ is the Tenant you selected.
4. The resources that _**TENANT\_NAME**_ (**uat-01**, in this example) has access to are displayed.

<figure><img src="../../.gitbook/assets/G2.png" alt=""><figcaption></figcaption></figure>
