# Helpdesk V1 to V2 Upgrade Guide

This guide covers upgrading from **Helpdesk V1** (the `Duplo.ai.studio` Windows service running on the DuploCloud master VM) to **Helpdesk V2** (a fully Kubernetes-native deployment managed via Helm, running inside a DuploCloud tenant).

This upgrade follows the **Integrated** deployment mode — V2 is connected to and managed by your existing DuploCloud master portal.

---

## What Changes

| | V1 | V2 |
|---|---|---|
| **Deployment** | Windows service on the master VM | Helm chart in a Kubernetes tenant |
| **Infrastructure** | Runs on the master host | Dedicated EKS nodes (ASG) |
| **Storage** | Local disk on master VM | EFS (Elastic File System) |
| **Load balancing** | Front door proxy on master VM | AWS ALB via Kubernetes Ingress |
| **Updates** | Manual service reinstall | `helm upgrade` |
| **Observability** | Windows Event Viewer | Kubernetes pod logs, DuploCloud portal |

V2 runs entirely within your AWS account inside a DuploCloud tenant. The master portal's front door proxy is updated to route `/v1/aistudio/*` traffic to the new V2 endpoint.

---

## Prerequisites

### Tools (DuploCloud Team)

| Tool | Version | Install |
|---|---|---|
| `aws` CLI | v2+ | `brew install awscli` |
| `kubectl` | v1.21+ | `brew install kubectl` |
| `helm` | v3+ | `brew install helm` |
| `python3` | v3.7+ | Built-in on macOS |

### Access Required

| Item | Required | Notes |
|---|---|---|
| DuploCloud master URL | ✅ | e.g. `https://duplo.yourcompany.com` — no trailing slash |
| DuploCloud API token | ✅ | Admin-level token from the master portal |
| AWS credentials for the master account | ✅ | See [Setting Up AWS Credentials](#setting-up-aws-credentials) below |
| `kubectl` access to the master EKS cluster | ✅ | See [Setting Up kubectl Access](#setting-up-kubectl-access) below |
| SSH / RDP access to the master VM | Optional | Required for V1 cleanup if SSM is not available |

### Information to Collect from the Customer

Before starting, gather the following:

| Item | Notes |
|---|---|
| DuploCloud portal URL | e.g. `https://duplo.yourcompany.com` |
| Admin API token | Generated in the portal under **Administrator → API Tokens** |
| Target AWS region | e.g. `us-east-1` |
| Portal domain for V2 Helpdesk | e.g. `helpdesk.yourcompany.com` |
| xterm subdomain | e.g. `xterm.helpdesk.yourcompany.com` |
| Google OAuth Client ID and Secret | See [Google OAuth Credentials](#google-oauth-credentials) below |
| Super-user email list | Comma-separated admin emails |
| Slack App Token + Bot Token | Only if enabling Slack integration |
| EC2 Instance ID of the master VM | For V1 service cleanup via SSM |

---

## Setting Up AWS Credentials

### Option A — Static IAM Credentials

If the customer provides an AWS access key and secret, configure a named profile:

```bash
aws configure --profile <profile-name>
```

You will be prompted for:
- AWS Access Key ID
- AWS Secret Access Key
- Default region (e.g. `us-east-1`)
- Output format (`json`)

Verify the profile works:
```bash
aws sts get-caller-identity --profile <profile-name>
```

### Option B — IAM Role Assumption (Recommended)

The customer can create an IAM role for DuploCloud to assume. Add this to `~/.aws/config`:

```ini
[profile helpdesk-installer]
role_arn = arn:aws:iam::<ACCOUNT_ID>:role/DuploCloud-AWS-Admin
source_profile = <your-base-profile>
region = us-east-1
```

The customer's IAM role trust policy must include your IAM user as an allowed principal:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<YOUR_ACCOUNT_ID>:user/<YOUR_USERNAME>"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

The easiest way for a customer to create this role is to run the **DuploCloud Access CloudFormation template** with `CreateAdminRole = true` and `CreateEKSAdminRole = true`. The stack outputs a Role ARN you can use directly.

Verify role assumption works:
```bash
aws sts get-caller-identity --profile helpdesk-installer
```

---

## Setting Up kubectl Access

Once AWS credentials are configured, generate a kubeconfig entry for the EKS cluster:

```bash
aws eks update-kubeconfig \
  --name <cluster-name> \
  --region <region> \
  --profile <profile-name> \
  --alias <friendly-name>
```

Verify connectivity:
```bash
kubectl get nodes
```

All nodes should show `Ready` status before proceeding with the upgrade.

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

Users log in with any Google account (Gmail or Google Workspace). Admin access is controlled by the super-user email list you provide.

---

## Upgrade Overview

The upgrade has five phases:

1. **Deploy V2** — provision a new DuploCloud tenant with EKS nodes, EFS storage, and deploy the V2 Helm chart
2. **Update front door proxy** — point the DuploCloud master portal's proxy to the V2 endpoint
3. **Enable AI feature flag** — verify `ENABLE_AI` is set in the master portal system settings
4. **Clean up V1** — stop, kill, and delete the `Duplo.ai.studio` Windows service from the master VM
5. **Update DNS** — point the portal domain to the new V2 ALB

---

## Phase 1 — Deploy Helpdesk V2

### Option A — Guided Installation via Claude Code Skill (Recommended)

The `helpdesk-install-skill` in the `ai-ops` repository handles the entire V2 deployment interactively.

```bash
cd /path/to/ai-ops
claude
```

Invoke the skill:

```
/helpdesk-install-skill
```

When prompted for deployment mode, select **INTEGRATED**. The skill will:

1. Verify prerequisites (`aws`, `kubectl`, `helm`)
2. Confirm AWS profile and Kubernetes context
3. Collect DuploCloud master URL, API token, and all configuration values
4. Provision a DuploCloud tenant (new or existing)
5. Create an ASG and wait for worker nodes to become Ready (~10 min)
6. Create an EFS filesystem and wait for mount targets (~10 min)
7. Install the EFS CSI driver if not already present
8. Create the EFS-backed StorageClass
9. Discover or request an ACM certificate
10. Discover subnets and security groups from the DuploCloud plan
11. Generate `<customerName>-values.yaml` with all substituted values
12. Deploy the Helm release via DuploCloud Flux API or local Helm

Once deployment succeeds, the skill automatically proceeds to Phases 2–4 below.

> **Note:** Add `*-values.yaml` to `.gitignore` — the file contains plaintext secrets.

---

### Option B — Manual Helm Deployment

If deploying manually, complete the following infrastructure steps first via the DuploCloud portal or API, then deploy with Helm.

#### Step 1 — Create a Tenant

In the DuploCloud portal → **Administrator → Tenants** → **+ Add Tenant**, create a new tenant (e.g. `helpdesk`) under your infrastructure plan.

#### Step 2 — Create Worker Nodes

In the tenant → **Cloud Services → Hosts**, create an ASG:

| Setting | Value |
|---|---|
| Instance type | `t3a.large` (minimum) |
| Desired capacity | 1 |
| Min / Max | 1 / 2 |
| Autoscaling | Enabled |
| OS | Amazon Linux 2023 |
| Encryption | KMS encrypted |

Wait until nodes show **Ready** in the portal before proceeding.

#### Step 3 — Create EFS Storage

In the tenant → **Cloud Services → Storage → EFS** → **+ Add**:

| Setting | Value |
|---|---|
| Name | `ai-storage` |
| Encrypted | Yes |
| Performance mode | General Purpose |
| Throughput mode | Elastic |

Wait until all mount targets show **Available** (~5–10 min).

#### Step 4 — Create StorageClass

```bash
kubectl apply -f - <<EOF
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: duploservices-helpdesk-ai-storage
  labels:
    duplocloud.net/owner: duplo
    duplocloud.net/tenantname: helpdesk
provisioner: efs.csi.aws.com
parameters:
  basePath: /dynamic_provisioning
  directoryPerms: '700'
  fileSystemId: <efs-filesystem-id>
  gidRangeEnd: '10000'
  gidRangeStart: '1000'
  provisioningMode: efs-ap
reclaimPolicy: Retain
volumeBindingMode: Immediate
EOF
```

#### Step 5 — Deploy via Helm

```bash
helm upgrade --install helpdesk oci://quay.io/duplocloud/helpdesk \
  --version <chart-version> \
  --namespace duploservices-helpdesk \
  --create-namespace \
  --values <customerName>-values.yaml \
  --wait \
  --timeout 10m
```

Verify:

```bash
kubectl get pods -n duploservices-helpdesk
kubectl get ingress -n duploservices-helpdesk
```

---

## Phase 2 — Update Front Door Proxy

Once V2 pods are running, update the DuploCloud master portal's front door proxy to route traffic to the new endpoint.

```bash
curl -s -X POST \
  -H "Authorization: Bearer $DUPLO_TOKEN" \
  -H "Content-Type: application/json" \
  "$DUPLO_MASTER_URL/v3/admin/frontdoor/config" \
  -d "{\"AiStudioEndpoint\":\"$AI_STUDIO_BASE_URL\"}"
```

> ⚠️ **The portal will be briefly unavailable (15–30 seconds)** while the front door container restarts to apply the new configuration.

Restart the front door container on the master VM via SSM:

```bash
# Send restart command
COMMAND_ID=$(aws ssm send-command \
  --instance-ids "$MASTER_INSTANCE_ID" \
  --document-name "AWS-RunShellScript" \
  --parameters 'commands=["docker rm -f duplo-frontdoor"]' \
  --query "Command.CommandId" --output text)

# Poll for completion
aws ssm get-command-invocation \
  --command-id "$COMMAND_ID" \
  --instance-id "$MASTER_INSTANCE_ID" \
  --query "{Status:Status,Output:StandardOutputContent}" \
  --output json
```

If SSM is not available, RDP into the master VM and run:

```bash
docker rm -f duplo-frontdoor
```

Docker will automatically restart the container with the updated configuration.

Verify the container is back up:

```bash
aws ssm send-command \
  --instance-ids "$MASTER_INSTANCE_ID" \
  --document-name "AWS-RunShellScript" \
  --parameters 'commands=["docker ps | grep duplo-frontdoor"]'
```

---

## Phase 3 — Enable AI Feature Flag

Verify the `ENABLE_AI` system flag is enabled in the master portal.

**Check current status:**

```bash
curl -s \
  -H "Authorization: Bearer $DUPLO_TOKEN" \
  "$DUPLO_MASTER_URL/v3/admin/systemSettings/config" \
  | python3 -c "
import sys, json
data = json.load(sys.stdin)
flag = [x for x in data if x.get('Type')=='Flags' and x.get('Key')=='ENABLE_AI']
print(flag[0].get('Value','not set') if flag else 'not found')
"
```

**Enable if not already set:**

```bash
curl -s -X POST \
  -H "Authorization: Bearer $DUPLO_TOKEN" \
  -H "Content-Type: application/json" \
  "$DUPLO_MASTER_URL/v3/admin/systemSettings/config" \
  --data-raw '{"Type":"Flags","Key":"ENABLE_AI","Value":"true"}'
```

Alternatively, enable via the portal: **Administrator → System Settings → System Config** → set `ENABLE_AI` to `true`.

---

## Phase 4 — Clean Up Helpdesk V1

Once V2 is confirmed healthy and the front door proxy is routing traffic correctly, decommission the V1 Windows service.

### Automated Cleanup via SSM (Preferred)

```bash
COMMAND_ID=$(aws ssm send-command \
  --instance-ids "$MASTER_INSTANCE_ID" \
  --document-name "AWS-RunPowerShellScript" \
  --parameters 'commands=[
    "Stop-Service -Name \"Duplo.ai.studio\" -Force",
    "Get-Process | Where-Object { $_.ProcessName -like \"*Duplo.ai.studio*\" -or $_.ProcessName -like \"*AiStudio*\" } | Stop-Process -Force -ErrorAction SilentlyContinue",
    "sc.exe delete \"Duplo.ai.studio\"",
    "Get-Service -Name \"Duplo.ai.studio\" -ErrorAction SilentlyContinue | Select-Object Name, Status"
  ]' \
  --comment "Helpdesk V1 cleanup" \
  --query "Command.CommandId" --output text)

# Poll for result (check every 5s, up to 2.5 minutes)
aws ssm get-command-invocation \
  --command-id "$COMMAND_ID" \
  --instance-id "$MASTER_INSTANCE_ID" \
  --query "{Status:Status,Output:StandardOutputContent,Error:StandardErrorContent}" \
  --output json
```

### Manual Cleanup via RDP (Fallback)

If SSM is unavailable, RDP into the master VM and run the following in an **elevated PowerShell session** (Run as Administrator):

```powershell
# Stop the service
Stop-Service -Name "Duplo.ai.studio" -Force

# Kill any remaining processes
Get-Process | Where-Object {
  $_.ProcessName -like "*Duplo.ai.studio*" -or
  $_.ProcessName -like "*AiStudio*"
} | Stop-Process -Force -ErrorAction SilentlyContinue

# Delete the service
sc.exe delete "Duplo.ai.studio"

# Verify the service is gone (expected: ServiceNotFound)
Get-Service -Name "Duplo.ai.studio" -ErrorAction SilentlyContinue
```

---

## Phase 5 — Update DNS

After the ALB is provisioned, get the ALB DNS name and update your DNS records:

```bash
kubectl get ingress -n duploservices-helpdesk \
  -o jsonpath='{.items[0].status.loadBalancer.ingress[0].hostname}'
```

Update your DNS provider:

| Type | Name | Value |
|---|---|---|
| CNAME | `helpdesk.yourcompany.com` | `<alb-dns>.us-east-1.elb.amazonaws.com` |
| CNAME | `xterm.helpdesk.yourcompany.com` | `<alb-dns>.us-east-1.elb.amazonaws.com` |

If using Route 53, use an **Alias A record** instead of a CNAME.

---

## Rollback Plan

If V2 deployment fails before V1 is decommissioned, V1 is still running and no rollback is needed — simply fix the V2 issue and retry.

If V1 has already been decommissioned:

1. Restore the front door proxy to point to V1 by reverting `AiStudioEndpoint`
2. On the master VM, reinstall the V1 service from the original installer
3. Investigate the V2 failure before retrying

---

## Verification Checklist

After completing all phases, verify the following:

- [ ] All V2 pods are Running: `kubectl get pods -n duploservices-helpdesk`
- [ ] Portal loads at the V2 URL (e.g. `https://helpdesk.yourcompany.com`)
- [ ] Login with Google OAuth works
- [ ] Front door proxy is routing to V2: the DuploCloud portal's AI Studio link opens V2
- [ ] `ENABLE_AI` flag is `true` in system settings
- [ ] V1 `Duplo.ai.studio` service is no longer present on the master VM
- [ ] DNS records point to the new ALB

---

## Troubleshooting

| Issue | Resolution |
|---|---|
| Pods stuck in `Pending` | Check EFS CSI driver: `kubectl get pods -n kube-system \| grep efs` |
| ALB not provisioned | Verify AWS Load Balancer Controller: `kubectl get pods -n kube-system \| grep aws-load-balancer` |
| Front door proxy not routing to V2 | Verify `AiStudioEndpoint` was saved and the container restarted |
| SSM cleanup fails | Fall back to RDP + manual PowerShell cleanup |
| V1 service not found on cleanup | V1 may have already been removed in a prior attempt — proceed |
| Portal shows 502 after front door restart | Wait 30–60 seconds for the container to fully restart |
