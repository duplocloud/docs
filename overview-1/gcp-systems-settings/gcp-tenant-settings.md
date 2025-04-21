---
description: Configure Tenant settings in the DuploCloud UI for GCP users
---

# GCP Tenant Settings

## Configuring Tenant settings:&#x20;

1. Navigate to **Administrator** -> **Tenants**.
2. In the **NAME** column, select the name of the Tenant you want to configure settings for.&#x20;
3. Select the **Settings** tab, and click **Add**. The **Add Tenant Feature** pane displays.
4. From the **Select Feature** list box, select the setting (see list of settings below).&#x20;
5. Click **Enable**, or enter an appropriate value.&#x20;
6. Click **Add**. The setting is applied to the Infrastructure.&#x20;

### Tenant settings

| **Delete Protection**                              | Enables delete protection for the Tenant.                                           |
| -------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Enable K8S network policy**                      | Enables Kubernetes network policies for the Tenant.                                 |
| **Enable option to run K8S pods on any host**      | Enables the option to run the Tenant's Kubernetes (K8S) pods on any available Host. |
| **Allow hosts to run K8S pods from other tenants** | Allows the Tenant's Hosts to run Kubernetes (K8S) pods from other Tenants.          |
| **Enable k8s job fault logging by default**        | Enables Kubernetes job fault logging by default for the Tenant.                     |
| **Enable Cluster Autoscaler OverProvisioning**     | Enables Cluster Autoscaler overprovisioning for the Tenant.                         |
| **Other**                                          | Allows entering a custom or unlisted setting.                                       |

