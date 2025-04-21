---
description: Configure Infrastructure settings in the DuploCloud UI for GCP users
---

# GCP Infrastructure Settings

## Configuring Infrastructure settings:&#x20;

1. Navigate to **Administrator** -> **Infrastructure**.
2. In the **NAME** column, select the name of the Infrastructure you want to configure settings for.&#x20;
3. Select the **Settings** tab, and click **Add**. The **Infra - Set Custom Data** pane displays.
4. From the **Setting Name** list box, select the setting (see list of settings below).&#x20;
5. Click **Enable**, or enter an appropriate value.&#x20;
6. Click **Set**. The setting is applied to the Infrastructure.&#x20;

### Infrastructure Settings

| **GKE Endpoint Visibility**        | Configures GKE endpoint visibility to public, private, or both.      |
| ---------------------------------- | -------------------------------------------------------------------- |
| **Cluster Autoscaler**             | Enables Cluster Autoscaler for the Infrastructure.                   |
| **GKE Minimum Ports Per VM**       | Specifies the minimum number of ports that must be available per VM. |
| **Enable Dynamic Port Allocation** | Enables dynamic port allocation.                                     |
| **Enable K8s Windows Workload**    | Enables Kubernetes support for Windows workloads.                    |
| **Other**                          | Allows configuring a custom or unlisted setting.                     |
