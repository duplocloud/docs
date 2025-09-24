---
description: Set quotas for resource allocation in a DuploCloud Plan
---

# Resource Quotas

An Administrator can define Quotas for resource allocation in a DuploCloud Plan. Quotas can restrict the total number of allowed resources by resource type, and, where applicable, by instance family and size.

Once the Quota is defined, DuploCloud cannot create new resources that exceed the quota configured in the Plan.

The quotas are applied at the Instance Family level. If you define a quota for `t4g.large`, it will be enforced for all smaller instances in the same family. For example, if the quota for `t4g.large` is set to `100`, the total number of instances in the `t4g` family (including `t4g.small` and `t4g.medium`) cannot exceed 100.

## Creating Resource Instance Quotas

Use an instance quota to limit the number of EC2, RDS, or ElastiCache instances of a specific family and size. This ensures resources within a particular instance family do not exceed the defined limit.

1. Navigate to **Administrator** → **Plans** in the DuploCloud Portal.
2. Select the **Plan** you want to configure.
3. Select the **Quota** tab.
4. Choose the tab representing the resource type (**EC2**, **RDS**, or **ElastiCache**).
5. Click **Add New Instance Quota**.
6. Select the instance family from the **Family** list box.
7. Select the instance size to restrict from the **Size** list box.
8. Enter the maximum number of instances allowed in the **Count** field. For effectively unlimited availability, enter a high number (e.g., `1000`).
9. Click **Add** to save the quota, and click **Update Plan** to apply the changes to the Plan.

<figure><img src="../../.gitbook/assets/Screenshot (182).png" alt=""><figcaption></figcaption></figure>

## Editing or Deleting a Resource Instance Quota

Follow these steps to modify or remove an existing instance quota.

1. Navigate to **Administrator** → **Plans**.
2. Select the **Plan** you want to configure.
3. Select the **Quota** tab.
4. Choose the tab for the resource type (**EC2**, **RDS**, or **ElastiCache**).
5. In the row of the instance quota you want to edit or delete, click the menu icon (<img src="../../.gitbook/assets/menu icon (24).avif" alt="" data-size="line">).
6. Select **Edit** to modify the quota or **Remove** to delete it.

## **Setting Cumulative Count Resource Quotas**

Use a cumulative count quota to limit the total number of a specific resource type that can be created in a Tenant. If no value is set, there is no limit.

1. Navigate to **Administrator** → **Plans** and select the **Plan** you want to configure.
2. Select the **Quota** tab.
3. Choose the tab for the desired resource type (e.g., **RDS**, **EC2**, **ElastiCache**, etc.).
4. Click **Update** next to **Cumulative Count**.
5. Enter the desired quota value in the **Cumulative Count** field. For effectively unlimited availability, enter a high number (e.g., `1000`).
6. Click **Set** to save the change.
7. Click **Update Plan** to apply the changes. Users cannot create new resources of this type once the cumulative count quota is reached.
