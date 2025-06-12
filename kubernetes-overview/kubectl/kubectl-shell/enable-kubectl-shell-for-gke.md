---
description: Configure the kubectl shell for for DuploCloud-managed GKE deployments
---

# Enable Kubectl Shell for GKE

Enabling `kubectl` shell access in GCP is part of a one-time DuploCloud Portal setup process.

## Prerequisite

**Ensure a Node Pool Exists:** Before creating the `k8s-shell` service, make sure that your GKE tenant has at least one node pool.

To check:

1. Go to **Kubernetes → Nodes** in the DuploCloud Portal.
2. If no nodes are listed, navigate to **Kubernetes → Node Pools** and click **Add** to create a new node pool.
   * Choose an appropriate **Instance Type** and **Node Count** (you can scale it down later).
   * Submit and wait for the nodes to become active.

Once a node pool is available, proceed to create the shell service.

## Step 1. Create a DuploCloud Service

1. From the **Tenant** list box, select the correct Tenant.
2. Navigate to **Kubernetes** -> **Services**.
3. Click **Add**. The **Add Service** page displays.&#x20;
4. Fill in the fields below. Leave any fields not listed at their default values.

<table data-header-hidden><thead><tr><th width="221.99993896484375">Add Service page field </th><th>Value</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td><code>k8s-shell</code></td></tr><tr><td><strong>Cloud</strong></td><td><code>Google</code></td></tr><tr><td><strong>Platform</strong></td><td><code>GKE Linux</code></td></tr><tr><td><strong>Docker Image</strong></td><td><code>duplocloud/shell:terraform-kubectl-latest</code></td></tr></tbody></table>

5. Enter the following in the **Environmental Variables** field:&#x20;

```
- Name: FLASK_APP_SECRET
  Value: b33d13ab-5b46-443d-a19d-asdfsd443
- Name: DUPLO_AUTH_URL
  Value: https://<CUSTOMER_NAME>.duplocloud.net
```

6. Click **Next**, and then **Create**.

## Step 2: Create a Load Balancer

1. From the DuploCloud Portal, navigate to **Kubernetes** -> **Services.**
2. From the **NAME** column, select the `k8s-shell` Service you created in the previous step.
3. Select the **Load Balancers** tab, and click **Configure Load Balancer**.&#x20;
4. Fill in the fields below. Leave any fields not listed at their default values.

<table data-header-hidden><thead><tr><th width="231.7777099609375"></th><th></th></tr></thead><tbody><tr><td><strong>Type</strong></td><td><code>Application LB</code></td></tr><tr><td><strong>Container port</strong></td><td><code>80</code></td></tr><tr><td><strong>Health Check</strong></td><td><code>/duplo_auth</code> </td></tr><tr><td><strong>Certificate</strong></td><td>Select your certificate from the list box. If none are present, you will need to configure a certificate. </td></tr><tr><td><strong>External port</strong></td><td><code>443</code></td></tr><tr><td><strong>Visibility</strong></td><td><code>Public</code></td></tr><tr><td><strong>Application mode</strong></td><td><code>Docker mode</code></td></tr><tr><td><strong>Health Check</strong></td><td><code>/duplo_auth</code></td></tr><tr><td><strong>Backend Protocol</strong></td><td><code>http</code></td></tr></tbody></table>

5. Click **Add**.

## Step 3: Add the DNS Name to System Settings

1. Navigate to **Administrator** -> **Systems Settings**.&#x20;
2. Select the **System Config** tab, and click **Add**. The **Add Config** pane displays.
3. Fill in the fields below.&#x20;

<table data-header-hidden><thead><tr><th width="164.22222900390625"></th><th></th></tr></thead><tbody><tr><td><strong>Config Type</strong></td><td><code>AppConfig</code></td></tr><tr><td><strong>Key</strong></td><td><code>Other</code></td></tr><tr><td><strong>Key</strong></td><td><code>DuploShellFqdn</code></td></tr><tr><td><strong>Value</strong></td><td>Paste the <strong>fully qualified DNS name*</strong> of your kubectl shell ingress/Load Balancer.<br>Example: <code>https://k8s-shell.example.duplocloud.net</code></td></tr></tbody></table>

{% hint style="info" %}
To find the DNS name, go to **Kubernetes** → **Services**, select the `k8s-shell` Service, then select the **Load Balancers** tab. Click the name of the Load Balancer, and copy the DNS name from the **DNS Name box**.&#x20;
{% endhint %}

4. Click **Submit**. Access to the `kubectl` shell is enabled.

