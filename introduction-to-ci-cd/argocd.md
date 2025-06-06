---
description: Deploy Argo CD in a DuploCloud-managed Infrastructure
---

# ArgoCD

[Argo CD](https://argo-cd.readthedocs.io/) is a declarative, GitOps-based continuous delivery (CD) tool for Kubernetes. It enables you to manage Kubernetes resources using Git repositories as the source of truth, allowing you to automate and track application deployments with version control and auditing.

DuploCloud integrates with Argo CD, allowing you to deploy and manage applications declaratively within your Duplo-managed infrastructure. This integration streamlines continuous delivery workflows, reduces manual configuration, and helps enforce consistent deployments across environments.

## Integrating Argo CD with DuploCloud

### Step 1: Create a Tenant for Argo CD

Navigate to **Administrator** → **Tenants** and click **Add** to create a dedicated Tenant for hosting Argo CD,  for example, `argocd01`.

### Step 2: Deploy Argo CD to the Tenant

Install Argo CD into your `argocd01` Tenant using the official [`argo-cd` Helm chart](https://artifacthub.io/packages/helm/argo/argo-cd). This will deploy all necessary Argo CD components, including the API server, UI, and controllers, into the Kubernetes namespace for the Tenant.

```bash
helm install argocd argo/argo-cd -n argocd01
```

Optionally, you can use DuploCloud’s [in-progress Terraform module](https://github.com/duplocloud/terraform-kubernetes-addons/pull/5) if it's available in your environment.

### Step 3: Configure Ingress and DNS

Expose the Argo CD UI via an Ingress controller:

* Ensure that a DNS name points to the ALB created by the Helm chart.
* You can configure this manually or use [External DNS](https://github.com/kubernetes-sigs/external-dns) if available.

### Step 4: Enable API Key Support for Admin

To allow DuploCloud to authenticate with Argo CD:

1. Locate the `argocd-cm` ConfigMap.
2. Add the following entry:

```yaml
accounts.admin: apiKey
```

This enables **API key support** for the admin account. No restart is required because Argo CD picks this up automatically.

### Step 5: Generate an Admin Token

1. Log into the Argo CD UI using the DNS name from above.
   * The default username is `admin`.
   * The initial password is in the Kubernetes secret named `argocd-initial-admin-secret`.
2. Navigate to **Settings** -> **Accounts** -> **admin** and generate a new token.

### Step 6: Configure DuploCloud to Use Argo CD

To enable DuploCloud to integrate with Argo CD, you'll need to add two custom system settings.

1. Navigate to **Administrator** → **Settings** → **System Settings**.
2. Click **Add**, The Add Config pane displays.
3. In the **Config Type** list box, select **Other**.&#x20;
4. In the **Other Config Type** field, enter `AppConfig/argocd`.
5. In the **Key** field, enter the key (including `INFRA_NAME`):
   * **For the endpoint**: `argocd/INFRA_NAME/endpoint`.
   * **For the token**: `argocd/INFRA_NAME/admin_token`.
6. In the **Value** field, enter the corresponding value:
   * **For the endpoint**: `https://DNS_NAME_FROM_STEP_4/`.
   * **For the token**: `Bearer TOKEN_FROM_STEP_5`. Make sure the token value begins with `Bearer`. This prefix is required and not included in the token generated by Argo CD.

### Step 7: Test the Integration

Go to **CI/CD** -> **Argo CD** in any Tenant within the `INFRA_NAME` infrastructure.

* If everything is configured correctly, you will see synced applications.
* If the token or endpoint are incorrect, you may see a "session" error.

### (Optional) Use the Argo CD CLI Inside the Pod

To troubleshoot or interact directly:

```bash
kubectl exec -it deploy/argocd-server -n argocd01 -- bash
argocd <ARGOCD_DNS_NAME>:443 --username admin
```

* You can list accounts:

```bash
argocd account list
```
