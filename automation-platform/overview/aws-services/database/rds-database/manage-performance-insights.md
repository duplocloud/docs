---
description: Manage Performance Insights for RDS databases in DuploCloud
---

# Manage Performance Insights

Performance Insights is an Amazon RDS feature that enables you to monitor and analyze the performance of your database. It provides key metrics and deep insights into database activity, helping you identify bottlenecks and optimize query performance. You can configure Performance Insights with DuploCloud when creating a new RDS instance and update them for an existing RDS instance .

## **Configuring Performance Insights**

When [creating a new RDS instance](../../../../../aws-user-guide/aws-services/database/rds-database/#id-0-toc-title), complete the following steps:

1. Enable the **Enable Performance Insights (Optional)** option.
2. &#x20;Set the retention period for Performance Insights data in the **Performance Insights Retention in Days (Optional)** field.&#x20;
3. Select an encryption key to encrypt Performance Insights data in the **Performance Insights Encryption (Optional)** list box.&#x20;

## Updating performance insights for an existing RDS

1. Select the Tenant from the **Tenant** list box.
2. In the DuploCloud Portal, navigate to **Cloud Services** -> **Database** and select the **RDS** tab.&#x20;
3. Click on the RDS name in the **NAME** column.
4. From the **Actions** menu, select **RDS Settings** and then **Update Performance Insights**. The **Update Performance Insights** pane displays.&#x20;
5. Select **Enable Performance Insights**.
6. In the **Performance Insights Retention in Days field**, enter a retention period (1–731 days).
7. From the **Performance Insights Encryption** list box, select an encryption key or select **No Encryption**.
8. **Click Update** to apply the changes.&#x20;
