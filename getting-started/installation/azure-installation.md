# Azure Installation Guide

This guide covers installing DuploCloud AI Helpdesk on **Azure Kubernetes Service (AKS)** using Terraform.

> **Note:** The guided skill-based installation (like the AWS `helpdesk-install-skill`) is currently in development for Azure. The current method uses Terraform automation. Contact your DuploCloud account team to schedule an installation.

---

## What Gets Deployed

Terraform provisions the following resources in order:

```
AKS Node Pool → Storage Class (conditional) → Namespace → ConfigMap → Helm Release
```

| Component | Azure Resource |
|---|---|
| **Backend** | ASP.NET Core API — tickets, projects, agent orchestration |
| **Frontend** | React web UI served via nginx |
| **MongoDB** | Kubernetes StatefulSet with Azure Blob NFS storage |
| **Web Terminal** | Browser-based terminal for agent command execution |
| **Duplo Agent** | Claude-powered AI agent (connects to Azure AI Foundry) |
| **Ingress** | Azure Application Gateway routing HTTPS traffic |
| **Persistent Storage** | Azure Blob NFS (`azureblob-nfs-premium`) for backend and agent |

All components run inside a dedicated namespace in your AKS cluster within your Azure subscription.

---

## Prerequisites

### Tools (DuploCloud Team)

| Tool | Version | Install |
|---|---|---|
| `git` | Any | `brew install git` |
| `terraform` | >= 1.5.0 | `brew install terraform` |
| `azure-cli` | >= 2.50 | `brew install azure-cli` |
| `kubectl` | >= 1.27 | `brew install kubectl` |
| `helm` | >= 3.12 | `brew install helm` |

### Azure Access Required

| Item | Required | Notes |
|---|---|---|
| Azure **Contributor** role on the AKS resource group | ✅ | Required for node pool creation |
| Kubernetes **cluster-admin** RBAC | ✅ | Required for namespace and storage class creation |
| Access to `oci://quay.io/duplocloud` Helm registry | ✅ | No credentials needed — public OCI registry |

---

## What the Customer Must Provide

Collect the following before starting:

| Item | Required | Notes |
|---|---|---|
| Azure Subscription ID | ✅ | e.g. `82300ad4-6ef0-48ef-acee-a4d9e495e5a4` |
| Resource group containing the AKS cluster | ✅ | e.g. `duploinfra-ai` |
| AKS cluster name | ✅ | e.g. `ai` |
| Azure region | ✅ | e.g. `westus`, `eastus` |
| Azure AI Foundry resource name | ✅ | The subdomain before `.services.ai.azure.com` |
| Azure AI Foundry API key | ✅ | From Keys and Endpoint in the Azure portal |
| Portal domain | ✅ | e.g. `helpdesk.yourcompany.com` |
| xterm subdomain | ✅ | e.g. `helpdesk-xterm.yourcompany.com` |
| Internal agent hostname | ✅ | e.g. `helpdesk-agent.yourcompany.com` |
| Google OAuth Client ID | ✅ | See [Google OAuth Credentials](#google-oauth-credentials) |
| Google OAuth Client Secret | ✅ | See [Google OAuth Credentials](#google-oauth-credentials) |
| Super-user email list | ✅ | Comma-separated admin emails |
| SSL certificate name on App Gateway | ✅ | The name of the cert configured in Azure Application Gateway |

---

## Google OAuth Credentials

DuploCloud AI Helpdesk uses Google OAuth for user authentication. Username/password login is not supported.

To create a Google OAuth client:

1. Go to [Google Cloud Console](https://console.cloud.google.com) → **APIs & Services** → **Credentials**
2. Click **Create Credentials** → **OAuth 2.0 Client ID**
3. Application type: **Web application**
4. Add the portal URL to **Authorized JavaScript origins** (e.g. `https://helpdesk.yourcompany.com`)
5. Add `https://helpdesk.yourcompany.com/auth/callback` to **Authorized redirect URIs**
6. Copy the **Client ID** and **Client Secret**

---

## Azure AI Foundry Configuration

DuploCloud AI Helpdesk uses **Azure AI Foundry** as the AI model backend. The API key is injected into the `duploAgent` component at deploy time.

### Finding Your Azure AI Foundry Details

1. Go to **Azure Portal → Azure AI Foundry**
2. Note the **Resource Name** — this is the subdomain before `.services.ai.azure.com` (e.g. if your endpoint is `https://my-foundry.services.ai.azure.com/anthropic`, the resource name is `my-foundry`)
3. Go to **Keys and Endpoint** and copy the **API Key**

### How It's Configured

The API key and endpoint URL are injected into the `duploAgent` pod as environment variables:

```yaml
duploAgent:
  extraEnv:
    - name: AZURE_API_KEY
      value: "<your-api-key>"
    - name: AZURE_BASE_URL
      value: "https://<resource-name>.services.ai.azure.com/anthropic"
```

These values are set via Terraform sensitive variables — the API key is never stored in `terraform.tfvars`.

> **Managed Identity (future):** Managed Identity authentication is also supported using `AZURE_CLIENT_ID` instead of `AZURE_API_KEY`. Contact your DuploCloud account team if your Azure setup uses Managed Identity.

---

## Step-by-Step Deployment

### Step 1 — Clone the Repository

```bash
git clone git@github.com:duplocloud-internal/azure-ai-hd-deployment-automation.git
cd azure-ai-hd-deployment-automation/helpdesk-terraform
```

### Step 2 — Log In to Azure and Get Cluster Credentials

```bash
az login
az account set --subscription "<subscription_id>"
az aks get-credentials --resource-group "<resource_group>" --name "<cluster_name>" --admin
```

Find your `kube_context` and `kube_config_path` for use in the next step:

```bash
kubectl config current-context   # e.g. "ai-admin"
echo $KUBECONFIG                 # if set, use this path; if empty, default is ~/.kube/config
```

Verify cluster access:
```bash
kubectl get nodes
```

> **Credential expiry:** If you get auth failures later, re-run `az aks get-credentials --overwrite-existing`.

### Step 3 — Check if Storage Class Exists

```bash
kubectl get storageclass azureblob-nfs-premium
```

- **Found** → set `create_storage_class = false` in `terraform.tfvars`
- **Not found** → set `create_storage_class = true`

### Step 4 — Edit `terraform.tfvars`

Open `terraform.tfvars` and fill in all values. **Do not put secrets here** — those go in Step 5.

```hcl
# Azure infrastructure
subscription_id  = "<subscription-id>"
resource_group   = "<resource-group>"
aks_cluster_name = "<cluster-name>"
location         = "westus"              # Azure region

# Kubernetes access
kube_config_path = "~/.kube/config"
kube_context     = "<from Step 2>"       # e.g. "ai-admin"

# Tenant
tenant_name = "<tenant>"                 # e.g. "helpdesk"
namespace   = "duploservices-<tenant>"

# Node pool
node_pool_name          = "helpdesk"
node_pool_vm_size       = "Standard_D2s_v3"
node_pool_min_count     = 2
node_pool_max_count     = 3
node_pool_desired_count = 2

# Azure AI Foundry
azure_foundry_resource_name = "<resource-name>"   # subdomain only, no URL

# Storage class
create_storage_class = false   # or true — from Step 3

# Helm chart version
helm_version = "0.1.51"

# URLs
frontend_url      = "https://helpdesk.<domain>"
frontend_hostname = "helpdesk.<domain>"
xterm_url         = "https://helpdesk-xterm.<domain>"
internal_hostname = "helpdesk-agent.<domain>"

# Admin access
auth_super_users = "admin@<domain>,ops@<domain>"
```

### Step 5 — Export Sensitive Variables

These **must never** be stored in `terraform.tfvars`. Export them as environment variables before running Terraform:

```bash
export TF_VAR_google_client_id="<google-client-id>"
export TF_VAR_google_client_secret="<google-client-secret>"
export TF_VAR_jwt_secret="$(openssl rand -base64 32 | tr -dc 'A-Za-z0-9' | head -c 32)"
export TF_VAR_mongodb_root_password="$(openssl rand -base64 24 | tr -dc 'A-Za-z0-9' | head -c 20)"
export TF_VAR_azure_foundry_api_key="<azure-ai-foundry-api-key>"
```

### Step 6 — Deploy

```bash
terraform init
terraform plan -out=plan.tfplan
terraform apply plan.tfplan
```

Deployment takes approximately **5–10 minutes**. The node pool provisioning is the main bottleneck.

### Step 7 — Verify

```bash
kubectl -n duploservices-<tenant> get pods
kubectl -n duploservices-<tenant> get ingress
helm -n duploservices-<tenant> list
```

All pods should reach `Running` status before proceeding.

### Step 8 — Configure DNS

Get the App Gateway IP from Terraform output:

```bash
terraform output app_gateway_ip
```

Add the following DNS records at your provider:

| Record Type | Name | Points To |
|---|---|---|
| A | `helpdesk.<domain>` | App Gateway public IP |
| A | `helpdesk-xterm.<domain>` | App Gateway public IP |
| A | `helpdesk-agent.<domain>` | App Gateway **private** IP |

> The internal agent hostname uses the App Gateway's **private** IP — it is not publicly accessible.

---

## Updating a Deployment

To update an existing deployment (e.g. new Helm chart version, config change):

```bash
cd azure-ai-hd-deployment-automation/helpdesk-terraform
git pull origin main

# Edit terraform.tfvars as needed
# Re-export any changed sensitive variables

terraform plan -out=plan.tfplan
terraform apply plan.tfplan
```

---

## Multi-Client Deployments

Each client needs its own tfvars file and Terraform state. Use `-var-file` to target a specific client:

```bash
terraform plan -var-file=envs/clientA.tfvars -out=plan.tfplan
terraform apply plan.tfplan
```

> Without a remote backend, deploying a different client from the same directory will overwrite local state. Use a remote backend (Azure Storage or Terraform Cloud) for production multi-client setups.

---

## Destroying a Deployment

```bash
terraform destroy
```

> **Warning:** MongoDB data will be lost if the persistent volume reclaim policy is `Delete`. Back up data before destroying.

---

## Ingress and SSL

Azure deployments use the **Azure Application Gateway** as the ingress controller. SSL termination is handled at the gateway using a pre-configured certificate.

The ingress annotations used:

```yaml
ingress:
  className: azure-application-gateway
  annotations:
    appgw.ingress.kubernetes.io/appgw-ssl-certificate: duplo   # cert name on App Gateway
    appgw.ingress.kubernetes.io/ssl-redirect: "true"
    appgw.ingress.kubernetes.io/request-timeout: "300"
    appgw.ingress.kubernetes.io/health-probe-status-codes: 200-503
```

The SSL certificate (`duplo` in the example above) must already be configured on the Azure Application Gateway before deployment. The customer must provide the certificate name.

---

## Troubleshooting

| Error | Resolution |
|---|---|
| `403 — cannot create namespaces/storageclasses` | Ensure `cluster-admin` RBAC is granted, or set `create_storage_class = false` |
| Helm timeout (>600s) | Node pool still scaling — run `kubectl get nodes -w` to monitor |
| `StorageClass already exists` | Set `create_storage_class = false` in tfvars |
| Provider auth failure | Re-run `az aks get-credentials --overwrite-existing`, verify `kube_context` in tfvars |
| `Namespace already exists` | Run `terraform import kubernetes_namespace_v1.helpdesk <namespace>` |
| Pods stuck in `Pending` | Check node pool status in Azure portal — node provisioning may still be in progress |
| 502 from App Gateway | Check pod health: `kubectl describe pods -n <namespace>` and verify health probe status codes annotation |
