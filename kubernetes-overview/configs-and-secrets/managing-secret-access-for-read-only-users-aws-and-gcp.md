---
description: >-
  Restrict or enable readonly access to Kubernetes Secrets and ConfigMap for AWS
  or GCP users.
---

# Managing Secrets and ConfigMaps access for readonly users (AWS and GCP)

Configure readonly user access to both Kubernetes Secrets and ConfigMaps using the **AllowReadonlyK8sSecrets** flag. This setting applies to all readonly users, whether they are Administrators, Tenants, or Users.

1. From the DuploCloud Portal, navigate to **Administrator** -> **Systems Settings**.
2.  Select the **System Config** tab, and click **Add**. The **Add Config** pane displays. \




    <div align="left"><figure><img src="../../.gitbook/assets/add config secret access.png" alt="" width="416"><figcaption><p>The <strong>Add Config</strong> pane </p></figcaption></figure></div>
3. In the **Config Type** list box, select **AppConfig**.
4. In the **Key** list box, select **Allow Readonly Users to view Kubernetes Secrets**.&#x20;
5. In the **Value** field, enter **True** or **False**. A true value allows readonly users to view Kubernetes Secrets and ConfigMaps. A false value prohibits readonly users from viewing Kubernetes Secrets and ConfigMaps.&#x20;
6. Click **Submit**. Readonly access to sensitive data in Kubernetes Secrets and ConfigMaps is configured.&#x20;

<figure><img src="../../.gitbook/assets/read only.png" alt=""><figcaption><p>The <strong>System Config</strong> page with the <strong>AllowReadonlyK8sSecrets</strong> flag set to False</p></figcaption></figure>

