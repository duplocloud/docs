---
description: Configuring backups for Kubernetes Secrets and ConfigMaps
---

# Backing Up and Restoring Kubernetes Secrets and ConfigMaps

DuploCloud provides automated infrastructure-level backups of Kubernetes Secrets and ConfigMaps across all tenants. These backups support disaster recovery, helping ensure that critical configuration and secret data can be restored if a tenant or infrastructure is lost. They also protect against accidental deletion or modification and support manual restoration when needed. All backups are securely stored in AWS S3.

{% hint style="info" %}
Backup support for Kubernetes Secrets and ConfigMaps is currently available only for **AWS**.
{% endhint %}

## Configuring Backups

Backups are configured via an infrastructure setting in the DuploCloud Portal:

1. Navigate to **Administrator** -> **Infrastructure**.
2. Select the Infrastructure you want to back up Secrets and ConfigMaps for in the **NAME** column.
3. Select the **Settings** tab.&#x20;
4.  Click **Add**. The **Infra - Set Custom Data** pane displays. \


    <div align="left"><figure><img src="../../../.gitbook/assets/Screenshot (791).png" alt=""><figcaption><p><strong>Infra - Set Custom Data</strong> pane</p></figcaption></figure></div>
5. In the **Setting Name** list box, select **Other**.&#x20;
6.  In the **Custom Setting** field, enter:&#x20;

    ```json
    ResourceBackupConfig
    ```
7. In the **Setting Value** field, enter:

```json
{ 
  "IsEnabled": true, 
  "IntervalInHours": "1", 
  "K8sResourceKinds": ["Secret", "ConfigMap"] 
}
```

8. Click **Set** to save the infrastructure setting.

{% hint style="info" %}
**Note**: The backup interval must be at least 1 hour. The `IntervalInHours` parameter accepts values in whole hours only; decimals are not permitted.
{% endhint %}

## Accessing Backups

Backups are saved automatically at the configured interval in the following S3 bucket and path structure:

```
s3://backups-duplo-xx/YEAR/MONTH/DATE/xx/infra/INFRANAME/k8s/namespaces/TENANTNAMES/
```

Backups run automatically, reflect resource changes or deletions, persist even if tenants or infrastructure are deleted, and support multiple AWS regions. Backup operations are tracked in logs and AWS CloudTrail.

{% hint style="info" %}
To restore Kubernetes Secrets or ConfigMaps from a backup, contact DuploCloud Support.
{% endhint %}
