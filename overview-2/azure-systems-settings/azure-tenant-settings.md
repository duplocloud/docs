---
description: Configure Tenant settings in the DuploCloud UI for Azure users
---

# Azure Tenant Settings

## Configuring Tenant settings:&#x20;

1. Navigate to **Administrator** -> **Tenants**.
2. In the **NAME** column, select the name of the Tenant you want to configure settings for.&#x20;
3. Select the **Settings** tab, and click **Add**. The **Add Tenant Feature** pane displays.
4. From the **Select Feature** list box, select the setting (see list of settings below).&#x20;
5. Select or deselect the **Enable** option, or enter an appropriate value.&#x20;
6. Click **Add**. The setting is applied to the Infrastructure.&#x20;

### Tenant Settings

| **Delete Protection**                                           | Enables delete protection for the Tenant.                                                                                    |
| --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Enable K8S network policy**                                   | Enables Kubernetes network policies for the Tenant.                                                                          |
| **Enable option to run K8S pods on any Host**                   | Enables the option to run the Tenant's Kubernetes (K8S) pods on any available Host.                                          |
| **Allow hosts to run K8S pods from other tenants**              | Allows the Tenant's Hosts to run Kubernetes (K8S) pods from other Tenants.                                                   |
| **Enable Azure MSSQL Server Audit**                             | Enables audits for Azure MSSQL Servers for the Tenant.                                                                       |
| **Enable Azure MSSQL Database Audit**                           | Enables audits for Azure MSSQL Databases for the Tenant.                                                                     |
| **Enable Azure MSSQL Transparent Data Encryption (TDE)**        | Enables Transparent Data Encryption (TDE) for Azure MSSQL Databases for the Tenant.                                          |
| **Enable Azure MSSQL Server Vulnerability Settings**            | Enables vulnerability settings for Azure MSSQL Servers for the Tenant.                                                       |
| **Enable Azure MSSQL Database Vulnerability Settings**          | Enables vulnerability settings for Azure MSSQL Databases for the Tenant.                                                     |
| **Enable Azure MSSQL Server Defender**                          | Enables Azure MSSQL Server Defender for the Tenant, providing threat protection.                                             |
| **Enable Azure VM Antimalware Extension**                       | Enables the Antimalware Extension for Azure VMs for the Tenant.                                                              |
| **Enable Azure VM Qualys Extension**                            | Enables the Qualys Extension for Azure VMs for the Tenant.                                                                   |
| **Enable Azure VM Dependency Agent Extension**                  | Enables the Dependency Agent Extension for Azure VMs for the Tenant.                                                         |
| **Enable Azure VM Diagnostic Agent Extension**                  | Enables the Diagnostic Agent Extension for Azure VMs for the Tenant.                                                         |
| **Enable Azure VM JIT Extension**                               | Enables Just-In-Time (JIT) access for Azure VMs for the Tenant.                                                              |
| **Enable Azure Storage Account Public Access**                  | Enables public access to Azure Storage Accounts for the Tenant.                                                              |
| **Enable Azure Storage Account Secure Transfer**                | Enables secure transfer (HTTPS) for Azure Storage Accounts for the Tenant.                                                   |
| **Allow Public Network Access for Databases and Cache Servers** | Enables public network access to databases and cache servers for the Tenant.                                                 |
| **Enable Application Gateway V2**                               | Enables the use of Application Gateway V2 for the Tenant, providing advanced traffic management and load balancing features. |
| **Enable k8s job fault logging by default**                     | Enables Kubernetes job fault logging by default for the Tenant, capturing and logging errors for easier troubleshooting.     |
| **Enable Cluster Autoscaler OverProvisioning**                  | Enables Cluster Autoscaler overprovisioning for the Tenant.                                                                  |
| Other                                                           | Allows entering a custom or unlisted setting.                                                                                |

