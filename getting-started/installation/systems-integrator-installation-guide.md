---
description: >-
  Cluster requirements, Helm values, and installation steps for systems
  integrators deploying DuploCloud AI HelpDesk on any Kubernetes cluster.
---

# Systems Integrator Installation Guide

DuploCloud AI HelpDesk is distributed as a single Helm chart and runs on **any conformant Kubernetes cluster**. The Kubernetes distribution is irrelevant — Amazon EKS, Azure AKS, Google GKE, self-managed Kubernetes on cloud VMs, and self-managed Kubernetes on-premises are all supported, as long as the cluster meets the requirements in this guide.

{% hint style="success" %}
**Bring your own Kubernetes.** This guide defines *what* the cluster must provide — an ingress controller, shared storage, block storage, TLS, DNS, an identity provider, and an LLM provider. *How* you satisfy each requirement is your decision. Where this guide names a specific product (Amazon EFS, ingress-nginx, Longhorn, and so on), it is an example of one way to meet the requirement, not a mandate.
{% endhint %}

## How this guide is organized

| Section                                                                                             | Purpose                                                                 |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| [1. Requirements](systems-integrator-installation-guide.md#id-1.-requirements)                      | What must exist before `helm install`                                   |
| [2. Helm values reference](systems-integrator-installation-guide.md#id-2.-helm-values-reference)    | How to configure the chart for your environment                         |
| [3. Install and configure](systems-integrator-installation-guide.md#id-3.-install-and-configure)    | Install the chart, create DNS records, verify, and configure the platform |
| [4. Tested configurations](systems-integrator-installation-guide.md#id-4.-tested-configurations)    | Worked examples per platform — informational, not prescriptive          |
| [5. Troubleshooting](systems-integrator-installation-guide.md#id-5.-troubleshooting)                | Common symptoms and fixes                                               |
| [6. Handoff and escalation](systems-integrator-installation-guide.md#id-6.-handoff-and-escalation)  | What to collect before contacting DuploCloud                            |
| [7. Uninstall](systems-integrator-installation-guide.md#id-7.-uninstall)                            | Removing the release and what it leaves behind                          |

{% hint style="info" %}
Replace every value in angle brackets, such as `<ADMIN_EMAIL>`, before applying commands or values files. Do not commit credentials, OAuth secrets, or MongoDB passwords to source control.
{% endhint %}

## Obtain from DuploCloud before you begin

* The Helm chart version to install.
* A **license token**. Without one the platform starts in a fail-closed state — see [1.12 License token](systems-integrator-installation-guide.md#id-1.12-license-token).
* Access to the chart registry if your network restricts outbound access to `quay.io`.

```bash
# Inspect the latest published chart
helm show chart oci://quay.io/duplocloud/helpdesk

# Inspect a specific version
helm show chart oci://quay.io/duplocloud/helpdesk --version <VERSION>
```

***

## 1. Requirements

Everything in this section must be in place **before** running `helm install`. The chart creates Kubernetes resources such as `Ingress` and `PersistentVolumeClaim` objects, but it does **not** install the controllers and drivers that fulfill them. Providing those is the integrator's responsibility.

### 1.1 Kubernetes cluster

| Requirement      | Detail                                                                                                            |
| ---------------- | ----------------------------------------------------------------------------------------------------------------- |
| Distribution     | Any conformant Kubernetes distribution — managed (EKS, AKS, GKE) or self-managed (cloud VMs or on-premises)       |
| Version          | 1.26 or later (tested through 1.36)                                                                               |
| Architecture     | `amd64` (x86-64) or `arm64` nodes                                                                                 |
| Nodes            | Minimum 2 for high availability; autoscaling to 6 or more recommended                                             |
| Node size        | 2 vCPU / 4 GiB minimum per node. Plan a baseline of roughly **2.1 vCPU** and **2.2 GiB** for the stack, excluding workload growth |
| Access           | A kubeconfig able to create the release namespace and all namespaced resources in it (Deployments, StatefulSets, Services, Ingress, PersistentVolumeClaims, Secrets, ConfigMaps, ServiceAccounts, CronJobs). The chart creates no cluster-scoped resources; cluster-wide permissions are needed only if you enable the optional bundled NFS server, which installs a `StorageClass` and `ClusterRole` |
| Tooling          | `kubectl` 1.26 or later and Helm 3.12 or later on the machine performing the install                              |

### 1.2 Ingress controller

The chart creates `Ingress` resources for the application, the web terminal, and (optionally) an internal endpoint for the agent. The cluster must provide a Layer 7 ingress controller that supports:

* Host-based routing
* WebSocket upgrades
* Request bodies of at least **50 MiB**
* Proxy buffers of at least **16 KiB** (OAuth callbacks carry large headers)
* Long read/send timeouts (3600 seconds recommended) for interactive agent sessions

Any controller that meets these requirements works. Set `ingress.className` and `ingress.annotations` to match the controller you choose. Examples that have been validated: AWS Load Balancer Controller (`alb`), ingress-nginx (`nginx`), and the GKE Gateway API (`gateway.enabled: true`).

### 1.3 Shared storage (ReadWriteMany)

The backend and the agent share files, so each needs a volume that can be mounted by more than one pod. The cluster must provide a `StorageClass` capable of provisioning **`ReadWriteMany` (RWX)** persistent volumes with:

| Requirement        | Detail                                                                                            |
| ------------------ | ------------------------------------------------------------------------------------------------- |
| Access mode        | `ReadWriteMany`                                                                                   |
| Filesystem         | POSIX semantics; files owned by UID/GID `1000` must be readable and writable by the pods          |
| Capacity           | At least **10 GiB** each for `backend.persistence` and `duploAgent.persistence`                   |
| Reclaim policy     | `Retain` recommended, so data survives accidental PVC deletion                                    |
| Volume expansion   | Recommended (`allowVolumeExpansion: true`)                                                        |
| Node prerequisites | If the storage is NFS-based, NFS client utilities (for example `nfs-common`) must be installed on every node |

Anything that satisfies these properties is acceptable — a cloud file service (Amazon EFS, Azure Files NFS, Google Filestore), an existing NFS appliance or server in your datacenter, a distributed filesystem (CephFS, Longhorn RWX, Portworx Sharedv4), or an NFS subdir provisioner backed by storage you already run.

{% hint style="warning" %}
The chart bundles an optional in-cluster NFS server (`nfs-server.enabled: true`). It exists for evaluation and proof-of-concept installs only and is **not production-grade**. It is never required — if you already have RWX-capable storage, use it and leave `nfs-server.enabled` at its default of `false`.
{% endhint %}

### 1.4 Block storage (ReadWriteOnce)

MongoDB, the MongoDB backup job, and ClickHouse (if enabled) each need a **`ReadWriteOnce` (RWO)** volume. Most clusters provide this through a default `StorageClass`; verify one exists, or set `mongodb.persistence.storageClass`, `mongodbBackup.storage.storageClass`, and `clickhouse.persistence.storageClass` explicitly.

| Volume                  | Minimum size | Notes                                                        |
| ----------------------- | ------------ | ------------------------------------------------------------ |
| MongoDB data            | 8 GiB        | Pin to a zone if your block storage is zonal                 |
| MongoDB backups         | 25 GiB       | Uses `WaitForFirstConsumer`; see the note on `--wait` below |
| ClickHouse (optional)   | 20 GiB       | Only when `clickhouse.enabled: true`                         |

### 1.5 Cluster autoscaler

If the node pool autoscales, a cluster autoscaler must be installed and configured for the cluster. This is not needed for fixed-size node pools.

### 1.6 TLS certificate

HTTPS is mandatory. Provide a certificate from a trusted certificate authority that covers **both** the application hostname and the web-terminal (xterm) hostname, using either:

* A cloud-managed certificate (for example ACM, Google-managed, or Azure Key Vault) referenced through ingress annotations, or
* A Kubernetes TLS `Secret` in the release namespace — for example issued through cert-manager — referenced through `ingress.tls`.

### 1.7 DNS

Two hostnames are required: one for the application and one for the web terminal (`xterm.hostname`). Create the DNS records **after** `helm install`, because the load-balancer address is only available once the ingress controller has reconciled the `Ingress`.

### 1.8 Identity provider

At least one of Google, Microsoft Entra, Okta, or Keycloak. Register the application with the redirect URI `https://<APP_HOSTNAME>/signin-<provider>` and set the matching chart values:

| Provider  | Redirect URI suffix | Helm values                                                                                                                              |
| --------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Google    | `/signin-google`    | `secrets.googleClientId`, `secrets.googleClientSecret`                                                                                   |
| Microsoft | `/signin-microsoft` | `secrets.microsoftClientId`, `secrets.microsoftClientSecret`, `secrets.microsoftTenantId`                                                |
| Okta      | `/signin-okta`      | `secrets.oktaClientId`, `secrets.oktaClientSecret`, `secrets.oktaDomain`                                                                 |
| Keycloak  | `/signin-keycloak`  | `secrets.keycloakAuthority`, `secrets.keycloakClientId`, `secrets.keycloakClientSecret`, `secrets.keycloakRealm`, `secrets.keycloakHost` |

Set `config.authAllowedOrigins` to the exact public frontend origin, including the scheme, and configure at least one superuser in `config.authSuperUsers` before the first login.

### 1.9 LLM provider

Choose one. The provider does not need to run in the same cloud as the cluster — an on-premises cluster can use Amazon Bedrock with static credentials, for example.

| Provider         | What is needed                                                                                                                                                                      | `CLAUDE_MODEL` format            |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| Amazon Bedrock   | IAM credentials (IRSA on EKS, or static access keys elsewhere) allowing `bedrock:InvokeModel` and `bedrock:InvokeModelWithResponseStream` on **both** `foundation-model/*` and `inference-profile/*` resources | `us.anthropic.claude-sonnet-4-6` |
| Azure AI Foundry | Foundry endpoint plus a managed identity or API key                                                                                                                                 | `claude-sonnet-4-6`              |
| GCP Vertex AI    | Claude enabled in the Vertex AI Model Garden (not yet fully supported)                                                                                                              | `claude-sonnet-4-6`              |
| Anthropic direct | API key (`sk-ant-...`)                                                                                                                                                              | `claude-sonnet-4-6`              |

{% hint style="warning" %}
The `CLAUDE_MODEL` format differs per provider. Using the wrong format causes silent failures.
{% endhint %}

### 1.10 Network egress

Pods need outbound access to:

* `quay.io` (container images and the Helm chart), plus any other registries you configure
* The chosen LLM provider's API endpoints
* The identity provider

Air-gapped deployment is not validated by this guide. Contact DuploCloud if you need to mirror images into a private registry.

### 1.11 Agent container privileges

The agent runs each ticket in an isolated sandbox and needs the `SYS_ADMIN` and `NET_ADMIN` Linux capabilities (the chart default). On some platforms the container must additionally run as root with `privileged: true` — see [Tested configurations](systems-integrator-installation-guide.md#id-4.-tested-configurations). Clusters enforcing Pod Security Admission need an exemption for the release namespace. Validate this with the cluster's security team before a production rollout.

### 1.12 License token

A license token issued by DuploCloud is **required**. Without a valid license the platform starts but runs **fail-closed**: users can sign in, but creating tickets, workspaces, providers, users, and other licensed resources is refused until a license is applied. Request the token from DuploCloud alongside the chart version.

There are two ways to apply it:

* **Helm values** — set `secrets.licensingToken` in `values.yaml` before install (or supply the `Licensing__Token` key yourself when you manage secrets externally — see [2.2](systems-integrator-installation-guide.md#id-2.2-auto-generated-secrets)).
* **From the UI** — after install, paste the token under **AI Admin → Access Control → License → Apply New License**. It takes effect immediately with no restart.

See [License](../../armor/access-control/license.md) for how licensing works, the UI walkthrough, and troubleshooting. Treat the token like any other credential and keep it out of source control.

***

## 2. Helm values reference

All configuration lives in a single `values.yaml`.

{% hint style="warning" %}
**The chart is the source of truth for values, not this page.** Available values and their defaults change between chart releases. Before you write your values file, pull the annotated defaults and the README from the exact chart version you are installing:

```bash
# Full values.yaml with a comment describing every key
helm show values oci://quay.io/duplocloud/helpdesk --version <VERSION> > helpdesk-values-defaults.yaml

# The chart's README, including per-platform examples
helm show readme oci://quay.io/duplocloud/helpdesk --version <VERSION> > helpdesk-README.md
```

Repeat this on every upgrade and diff against your values file. The tables below cover the values an integrator must decide on; treat the defaults shown as illustrative and defer to `helm show values` where they differ.
{% endhint %}

### 2.1 Required values

| Key                          | Description                                                                        | Example                        |
| ---------------------------- | ---------------------------------------------------------------------------------- | ------------------------------ |
| `config.authFrontendBaseUrl` | Public URL of the app. Used for OAuth redirects and CORS.                          | `https://helpdesk.example.com` |
| `config.authAllowedOrigins`  | CORS allowed origin. Must match `authFrontendBaseUrl` exactly. Single origin only. | `https://helpdesk.example.com` |
| `config.authSuperUsers`      | Comma-separated emails granted super-admin on first login.                         | `admin@example.com`            |
| `config.infraRegion`         | Cloud region. Used for Bedrock endpoint routing.                                   | `us-west-2`                    |
| `secrets.licensingToken`     | License token issued by DuploCloud. Without it the platform starts fail-closed; an admin can still sign in and apply a license from the UI. | `<LICENSE_TOKEN>` |
| `mongodb.auth.rootPassword`  | MongoDB root password.                                                             | `openssl rand -hex 16`         |
| `xterm.hostname`             | Hostname for the web terminal (separate ingress rule).                             | `xterm.example.com`            |

### 2.2 Auto-generated secrets

These generate automatically on first install and persist across upgrades. Do **not** set them unless you need deterministic values.

| Key                           | Behavior                                                                      | Warning                                                                        |
| ----------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| `secrets.jwtSharedSecret`     | Auto-generated (48-char alphanumeric). Persists via Secret lookup on upgrade. |                                                                                |
| `secrets.encryptionMasterKey` | Auto-generated (96 bytes base64). Persists via Secret lookup on upgrade.      | **Never change after first install** — makes all encrypted data unrecoverable. |

**External secret management:** set `secrets.existingSecret` to the name of a pre-existing Kubernetes `Secret` to skip chart-managed secret creation entirely. The external Secret must contain all required keys, including `Licensing__Token` (see the chart's `templates/secret.yaml` for exact key names). Use this with Vault, External Secrets Operator, or Sealed Secrets.

### 2.3 Identity / SSO

See [1.8 Identity provider](systems-integrator-installation-guide.md#id-1.8-identity-provider) for redirect URI patterns. Set the values for your chosen provider(s):

```yaml
secrets:
  # Google
  googleClientId: ""
  googleClientSecret: ""
  # Microsoft Entra
  microsoftClientId: ""
  microsoftClientSecret: ""
  microsoftTenantId: ""
  # Okta
  oktaClientId: ""
  oktaClientSecret: ""
  oktaDomain: ""
  # Keycloak
  keycloakAuthority: ""
  keycloakClientId: ""
  keycloakClientSecret: ""
  keycloakRealm: ""
  keycloakHost: ""
```

Optional IdP group sync:

```yaml
config:
  authIdpSyncAzureAdEnabled: "true"
  authIdpSyncAzureAdAdminGroupName: "HelpDesk-Admin"
  authIdpSyncAzureAdUserGroupPrefix: "HelpDesk-UG-"
```

### 2.4 Storage

Point the chart at the `StorageClass` names you provisioned in [1.3](systems-integrator-installation-guide.md#id-1.3-shared-storage-readwritemany) and [1.4](systems-integrator-installation-guide.md#id-1.4-block-storage-readwriteonce).

| Key                                   | Description                                                                          | Default                |
| ------------------------------------- | ------------------------------------------------------------------------------------ | ---------------------- |
| `backend.persistence.enabled`         | Enable the shared RWX volume                                                         | `true`                 |
| `backend.persistence.storageClass`    | RWX StorageClass name                                                                | `""` (cluster default) |
| `backend.persistence.size`            | RWX volume size                                                                      | `10Gi`                 |
| `backend.persistence.accessModes`     | Must be `[ReadWriteMany]`                                                            | `[ReadWriteMany]`      |
| `duploAgent.persistence.storageClass` | Agent's own PVC StorageClass. Set to the RWX class to avoid `WaitForFirstConsumer` issues. | `""`             |
| `mongodb.persistence.size`            | MongoDB data volume                                                                  | `8Gi`                  |
| `mongodb.persistence.storageClass`    | RWO StorageClass                                                                     | `""` (cluster default) |
| `mongodbBackup.enabled`               | Enable the backup CronJob                                                            | `true`                 |
| `mongodbBackup.schedule`              | Cron schedule                                                                        | `0 0 * * *`            |
| `mongodbBackup.storage.size`          | Backup volume size                                                                   | `25Gi`                 |
| `nfs-server.enabled`                  | Enable the bundled NFS server (evaluation only; see [1.3](systems-integrator-installation-guide.md#id-1.3-shared-storage-readwritemany)) | `false` |
| `nfs-server.storageClass.name`        | StorageClass name created by the bundled NFS server                                  | `nfs`                  |

{% hint style="warning" %}
The backup PVC uses `WaitForFirstConsumer`. Do **not** use `helm install --wait` — it will time out waiting for this PVC.
{% endhint %}

### 2.5 Ingress

| Key                         | Description                                                           | Default                          |
| --------------------------- | --------------------------------------------------------------------- | -------------------------------- |
| `ingress.enabled`           | Enable the external Ingress                                           | `true`                           |
| `ingress.className`         | Ingress class of the controller you installed                         | `alb`                            |
| `ingress.annotations`       | Controller-specific annotations (certificate reference, buffer size, body size, timeouts) | `{}`         |
| `ingress.tls`               | TLS config. Leave empty when TLS terminates at an upstream load balancer. | `[]`                         |
| `internalIngress.enabled`   | Enable an internal-only Ingress for the agent                         | `true`                           |
| `internalIngress.className` | Must match your internal ingress class                                | `alb`                            |
| `gateway.enabled`           | Use the Kubernetes Gateway API instead of Ingress (GKE)               | `false`                          |
| `gateway.className`         | GatewayClass name                                                     | `gke-l7-global-external-managed` |

Whatever controller you use, make sure its configuration satisfies the limits in [1.2](systems-integrator-installation-guide.md#id-1.2-ingress-controller). For ingress-nginx, that looks like:

```yaml
ingress:
  className: nginx
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    nginx.ingress.kubernetes.io/proxy-body-size: "50m"
    nginx.ingress.kubernetes.io/proxy-buffer-size: "16k"
    nginx.ingress.kubernetes.io/proxy-read-timeout: "3600"
    nginx.ingress.kubernetes.io/proxy-send-timeout: "3600"
```

### 2.6 LLM provider

{% tabs %}
{% tab title="Amazon Bedrock (IRSA)" %}

For clusters on EKS with an OIDC provider. The IAM policy must allow `foundation-model/*` **and** `inference-profile/*`.

```yaml
bedrockSubscription:
  enabled: true
  serviceAccount:
    irsaRoleArn: "<ROLE_ARN>"

duploAgent:
  serviceAccount:
    irsaRoleArn: "<ROLE_ARN>"
  extraEnv:
    - name: CLAUDE_MODEL
      value: "us.anthropic.claude-sonnet-4-6"
    - name: AWS_REGION
      value: "us-west-2"
```

{% endtab %}

{% tab title="Amazon Bedrock (static keys)" %}

For any cluster not on AWS — on-premises, AKS, GKE, or self-managed.

```yaml
bedrockSubscription:
  enabled: false
duploAgent:
  extraEnv:
    - name: CLAUDE_MODEL
      value: "us.anthropic.claude-sonnet-4-6"
    - name: AWS_ACCESS_KEY_ID
      value: "<KEY>"
    - name: AWS_SECRET_ACCESS_KEY
      value: "<SECRET>"
    - name: AWS_REGION
      value: "us-west-2"
```

{% endtab %}

{% tab title="Azure AI Foundry" %}

```yaml
config:
  azureBaseUrl: "https://<RESOURCE>.services.ai.azure.com/anthropic"
secrets:
  azureClientId: "<MANAGED_IDENTITY_CLIENT_ID>"   # Or azureApiKey for API-key auth
bedrockSubscription:
  enabled: false
duploAgent:
  extraEnv:
    - name: CLAUDE_MODEL
      value: "claude-sonnet-4-6"
    - name: AZURE_BASE_URL
      value: "https://<RESOURCE>.services.ai.azure.com/anthropic"
```

{% endtab %}

{% tab title="Anthropic direct" %}

```yaml
bedrockSubscription:
  enabled: false
duploAgent:
  extraEnv:
    - name: ANTHROPIC_API_KEY
      value: "sk-ant-..."
    - name: CLAUDE_MODEL
      value: "claude-sonnet-4-6"
```

{% endtab %}
{% endtabs %}

### 2.7 Components

| Component            | Default | Key                           |
| -------------------- | ------- | ----------------------------- |
| Backend              | always  | –                             |
| Frontend             | always  | –                             |
| MongoDB              | `true`  | `mongodb.enabled`             |
| Agent                | `true`  | `duploAgent.enabled`          |
| Helpdesk MCP         | `true`  | `helpdeskMcp.enabled`         |
| Core MCP             | `false` | `coreMcp.enabled`             |
| Slack Backend        | `true`  | `slackBackend.enabled`        |
| Teams Backend        | `false` | `teamsBackend.enabled`        |
| XTerm                | `true`  | `xterm.enabled`               |
| Bedrock Subscription | `true`  | `bedrockSubscription.enabled` |
| Collector            | `false` | `collector.enabled`           |
| NFS Server           | `false` | `nfs-server.enabled`          |
| ClickHouse           | `false` | `clickhouse.enabled`          |
| Internal Ingress     | `true`  | `internalIngress.enabled`     |
| Gateway API          | `false` | `gateway.enabled`             |

### 2.8 Tolerations and scheduling

The chart ships `dedicated=hd:NoSchedule` as the default toleration via a YAML anchor. Subcharts (MongoDB, NFS server, ClickHouse) do not inherit values from the parent, so overrides must be repeated on each.

| Scenario                   | Configuration                                                                                                         |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Dedicated tainted nodes    | Leave the default — tolerations match automatically                                                                   |
| Shared cluster (no taints) | Override `tolerations: []` at the top level **and** on each subchart (`mongodb.tolerations: []`, `nfs-server.tolerations: []`) |

To use a different taint key and keep the subcharts aligned:

```yaml
tolerations: &hdTolerations
  - key: "workload"
    operator: "Equal"
    value: "helpdesk"
    effect: "NoSchedule"
mongodb:
  tolerations: *hdTolerations
nfs-server:
  tolerations: *hdTolerations
```

### 2.9 Reference values file

A platform-neutral starting point. Replace all `<PLACEHOLDER>` values before use, then layer on the ingress annotations and LLM settings for your environment. Check it against `helm show values` for your chart version — keys can be added, renamed, or removed between releases.

```yaml
config:
  authFrontendBaseUrl: "https://<APP_HOSTNAME>"
  authAllowedOrigins: "https://<APP_HOSTNAME>"
  authSuperUsers: "<ADMIN_EMAIL>"
  infraRegion: "<REGION>"
  aiStudioIsMasterDisabled: true

secrets:
  licensingToken: "<LICENSE_TOKEN>"          # required -- issued by DuploCloud
  # jwtSharedSecret and encryptionMasterKey auto-generate -- do not set unless needed
  googleClientId: "<GOOGLE_CLIENT_ID>"
  googleClientSecret: "<GOOGLE_CLIENT_SECRET>"

mongodb:
  auth:
    rootUser: authuser
    rootPassword: "<MONGODB_PASSWORD>"       # openssl rand -hex 16
  persistence:
    enabled: true
    size: 8Gi
    storageClass: "<RWO_STORAGECLASS>"       # omit to use the cluster default

mongodbBackup:
  enabled: true
  schedule: "0 2 * * *"
  storage:
    size: 25Gi

backend:
  persistence:
    enabled: true
    storageClass: "<RWX_STORAGECLASS>"       # the ReadWriteMany class you provisioned
    accessModes: [ReadWriteMany]
    size: 10Gi

duploAgent:
  persistence:
    storageClass: "<RWX_STORAGECLASS>"
  extraEnv:
    # --- Choose ONE LLM provider (see 2.6) ---
    - name: CLAUDE_MODEL
      value: "us.anthropic.claude-sonnet-4-6"
    - name: AWS_REGION
      value: "<REGION>"

xterm:
  hostname: "<XTERM_HOSTNAME>"

ingress:
  enabled: true
  className: "<INGRESS_CLASS>"               # the class of the controller you installed
  annotations: {}                            # controller-specific annotations (see 1.2 and 2.5)
  tls: []                                    # set when TLS terminates at the ingress

internalIngress:
  enabled: false                             # true if you need an internal load balancer for the agent

bedrockSubscription:
  enabled: true                              # false if not using Bedrock via IRSA

slackBackend:
  enabled: false
teamsBackend:
  enabled: false
collector:
  enabled: false
coreMcp:
  enabled: false
clickhouse:
  enabled: false
```

***

## 3. Install and configure

### 3.1 Install the Helm chart

```bash
helm install helpdesk oci://quay.io/duplocloud/helpdesk \
  --version <VERSION> \
  --namespace helpdesk --create-namespace \
  --values values.yaml \
  --timeout 10m

kubectl get pods -n helpdesk -w
```

{% hint style="warning" %}
Do **not** use `--wait`. The backup PVC uses `WaitForFirstConsumer` and will cause a timeout.
{% endhint %}

### 3.2 Create DNS records

After install, read the load-balancer address and create DNS records:

```bash
kubectl get ingress -n helpdesk -o jsonpath='{.items[0].status.loadBalancer.ingress[0].hostname}'
# Or .ip for platforms that assign IPs
```

Create CNAME (or A) records for both hostnames pointing to this address.

### 3.3 Verify infrastructure

```bash
# All pods Running
kubectl get pods -n helpdesk

# All PVCs Bound
kubectl get pvc -n helpdesk

# Backend health
kubectl exec -n helpdesk deploy/helpdesk-backend -- curl -sf http://localhost:60021/healthz

# Agent health
kubectl exec -n helpdesk deploy/helpdesk-duplo-agent -- curl -sf http://localhost:8000/health

# HTTPS responds
curl -sI https://<APP_HOSTNAME> | head -5
```

### 3.4 Post-install platform configuration

After pods are healthy and login works, configure the platform through the UI. Each step links to the page that covers it in detail.

| Step                  | Where                                        | Key details                                                                                                                                         | Reference                                                              |
| --------------------- | -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| 1. Login              | Browser → app URL                            | Sign in as a `config.authSuperUsers` email via your IdP                                                                                             | [Access Control](../../armor/access-control/README.md)                 |
| 2. Verify license     | AI Admin → Access Control → License          | Status should read **Active**. If not, apply the token here.                                                                                        | [License](../../armor/access-control/license.md)                       |
| 3. Create LLM Model   | AI Admin → LLMs → + Add                      | **Model ID must match the `CLAUDE_MODEL` env var exactly**                                                                                          | [LLM Models](../../armor/agents/llm-models.md)                         |
| 4. Create Agent       | AI Admin → Agents → + Add                    | Endpoint: `http://<RELEASE>-duplo-agent:8000` (base URL only). Set `endpointDetails.path: api/sendMessage`. Set `metaData.STREAMING_ENABLED: true`. | [Duplo DevOps Agent](../../armor/agents/README.md)                     |
| 5. Create LLM Mapping | LLMs → LLM Mappings → + Add                  | Map model + agent pair. Scope: Workspace. Target: your workspace.                                                                                   | [LLM Models](../../armor/agents/llm-models.md)                         |
| 6. Create Skill       | AI Admin → Skills → + Add                    | Provide name + markdown description (`skillMd` field)                                                                                               | [Skills](../../armor/skills/README.md)                                 |
| 7. Create Persona     | AI Admin → Personas → + Add                  | Link skill(s)                                                                                                                                       | [Personas](../../armor/personas.md)                                    |
| 8. Create Provider    | AI Admin → Providers → + Add                 | Connect the cloud account or Kubernetes cluster the agent will operate on                                                                           | [Integrating Providers](../integrating-providers/README.md)            |
| 9. Create Scope       | During provider creation                     | Links credentials to a named scope                                                                                                                  | [Integrating Providers](../integrating-providers/README.md)            |
| 10. Create Workspace  | AI Admin → Workspaces → + Add                | Link persona(s), then add agent and scope(s)                                                                                                        | [Workspaces](../../armor/workspaces.md)                                |
| 11. Test              | AI DevOps → select workspace → create ticket | Verify the agent responds with LLM-generated content                                                                                                | [Tickets](../../armor/tickets.md)                                      |

***

## 4. Tested configurations

{% hint style="info" %}
The configurations below are ones DuploCloud has validated end to end. They are **worked examples**, not requirements. Any cluster that meets [Section 1](systems-integrator-installation-guide.md#id-1.-requirements) is supported, regardless of distribution or which products you choose to satisfy each requirement. The Helm values and post-install steps are the same everywhere — only the items listed here differ.
{% endhint %}

{% tabs %}
{% tab title="Amazon EKS" %}

| Topic             | Detail                                                                                                                      |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **Tested**        | 2026-09-15, Kubernetes 1.35                                                                                                 |
| **Ingress**       | AWS Load Balancer Controller. `ingress.className: alb` with ALB annotations (certificate ARN, scheme, subnets, target-type). |
| **RWX storage**   | Amazon EFS via the EFS CSI driver, StorageClass with `provisioningMode: efs-ap`. The EFS CSI controller needs its own IRSA role. |
| **RWO storage**   | EBS CSI driver (required as a separate add-on on Kubernetes 1.35+). Mark `gp2` or `gp3` as the default StorageClass.        |
| **LLM**           | Amazon Bedrock via IRSA. IAM policy must include `foundation-model/*` **and** `inference-profile/*` resources.               |
| **Agent sandbox** | `SYS_ADMIN` + `NET_ADMIN` capabilities work without `privileged: true`.                                                     |
| **OIDC**          | Must be enabled on the cluster for IRSA.                                                                                    |

{% endtab %}

{% tab title="Azure AKS" %}

| Topic                 | Detail                                                                                                                                                                    |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Tested**            | 2026-09-16, Kubernetes 1.35                                                                                                                                               |
| **Ingress**           | ingress-nginx installed via Helm; Azure Load Balancer assigns a public IP.                                                                                                |
| **RWX storage**       | Azure Files NFS via the Azure Files CSI driver.                                                                                                                           |
| **LLM**               | Azure AI Foundry (recommended) or Amazon Bedrock via static keys.                                                                                                         |
| **Agent sandbox**     | The agent runs as UID 1001 by default — override with `runAsUser: 0` + `privileged: true` for the sandbox to work. Capabilities are dropped for non-root users even with `privileged` set. |

{% endtab %}

{% tab title="Google GKE" %}

| Topic                  | Detail                                                                                                                                      |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Tested**             | 2026-09-17, Kubernetes 1.35                                                                                                                 |
| **Ingress**            | ingress-nginx installed via Helm, or the GKE Gateway API natively (`gateway.enabled: true`).                                                 |
| **RWX storage**        | Google Filestore via the Filestore CSI driver.                                                                                              |
| **LLM**                | Vertex AI (when Claude is enabled in your project) or Amazon Bedrock via static keys.                                                        |
| **Agent sandbox**      | Same as AKS — `runAsUser: 0` + `privileged: true` required.                                                                                 |
| **GCP cloud provider** | **Not yet implemented.** The Kubernetes scope works for cluster operations. GCP-native resource queries (Compute Engine, GCS, etc.) are not supported. |

{% endtab %}

{% tab title="Self-managed (cloud VMs or on-premises)" %}

Applies to any Kubernetes you operate yourself, whatever the distribution or where the nodes run.

| Topic             | Detail                                                                                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Tested**        | 2026-09-16, Kubernetes 1.36                                                                                                                                        |
| **Ingress**       | ingress-nginx. On clusters without a cloud load balancer, run the controller with `hostNetwork: true` as a `DaemonSet`, or front it with your own load balancer (MetalLB, hardware appliance, and so on). |
| **RWX storage**   | Any RWX-capable StorageClass — an existing NFS appliance or server, CephFS, Longhorn, Portworx, or similar. If NFS-based, install NFS client utilities on every node. The chart's bundled NFS server is acceptable for evaluation only. |
| **RWO storage**   | Any RWO StorageClass your distribution provides (local-path provisioner, Longhorn, SAN-backed CSI, and so on). Set it as the cluster default or reference it explicitly. |
| **LLM**           | Amazon Bedrock via static keys, Azure AI Foundry, or the Anthropic API directly.                                                                                  |
| **Agent sandbox** | `privileged: true` + `runAsUser: 0` required.                                                                                                                      |

{% endtab %}
{% endtabs %}

### Agent sandbox override

Where a platform requires the agent to run as root, set it in values rather than patching the deployment after install, so upgrades preserve it:

```yaml
duploAgent:
  securityContext:
    privileged: true
    runAsUser: 0
    runAsGroup: 0
    seccompProfile:
      type: Unconfined
    capabilities:
      add:
        - SYS_ADMIN
        - NET_ADMIN
```

***

## 5. Troubleshooting

| Symptom                               | Cause                                                              | Fix                                                                                  |
| ------------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| Creates refused (tickets, workspaces) | No valid license in force — missing, expired, or issued for a different host | Apply the license from AI Admin → Access Control → License, or set `secrets.licensingToken` and upgrade the release |
| Pods `Pending` on tolerations         | Node taint doesn't match the chart default `dedicated=hd:NoSchedule` | Set `tolerations: []` in values (and on each subchart) if no taints are used       |
| Pods `Pending` on capacity            | Insufficient node resources                                        | Check node capacity and autoscaler configuration                                     |
| PVC stuck `Pending`                   | No matching StorageClass, or `WaitForFirstConsumer` with no consumer | Verify the StorageClass exists and supports the required access mode; for the backup PVC, don't use `--wait` |
| RWX mount fails (`bad option`)        | NFS client not installed on the node                               | Install NFS client utilities on every node (for example `nfs-common` on Debian/Ubuntu) |
| MongoDB cannot schedule               | RWO volume pinned to a different zone than available nodes         | Check StorageClass zone affinity                                                     |
| `bwrap` permission denied             | Agent needs `SYS_ADMIN` as root                                    | Set `runAsUser: 0`, `privileged: true` on the agent container                        |
| OAuth redirect error (400)            | Wrong redirect URI in the IdP                                      | Must be `https://<HOST>/signin-<provider>` exactly; CORS origin must match exactly   |
| 502 Bad Gateway on login              | Proxy buffer too small for auth headers                            | Raise the ingress proxy buffer size to at least 16 KiB                               |
| 413 or header errors                  | Ingress body size or buffer limits                                 | Allow a 50 MiB request body and a 16 KiB proxy buffer                                |
| LLM `AccessDeniedException`           | Bedrock IAM missing `inference-profile/*`                          | Add both `foundation-model/*` and `inference-profile/*` to the IAM policy            |
| Wrong `CLAUDE_MODEL` format           | Model ID doesn't match the provider                                | Bedrock: `us.anthropic.claude-*`; Azure/Anthropic: `claude-*`                        |
| Agent 404 on ticket                   | Agent endpoint includes the full path                              | Endpoint should be the base URL only; set `endpointDetails.path: api/sendMessage`    |
| LLM dropdown empty in ticket UI       | No LLM Model + Mapping configured                                  | Create Model → LLM Mapping → link to workspace ([3.4](systems-integrator-installation-guide.md#id-3.4-post-install-platform-configuration)) |
| Image pull failures                   | No egress to `quay.io` or required registries                      | Allow outbound access or mirror images                                               |
| `helm install --wait` timeout         | Backup PVC `WaitForFirstConsumer`                                  | Don't use `--wait` on initial install                                                |
| Encrypted data unreadable             | `encryptionMasterKey` was changed                                  | **Never change this key after first install**                                        |

***

## 6. Handoff and escalation

When a step fails, collect:

```bash
kubectl get pods -n helpdesk -o wide
kubectl get events -n helpdesk --sort-by='.lastTimestamp' | tail -50
kubectl describe pod -n helpdesk <FAILING_POD>
kubectl logs -n helpdesk <FAILING_POD> --tail=200
kubectl logs -n helpdesk <FAILING_POD> --previous --tail=200
kubectl get pvc -n helpdesk
kubectl get ingress -n helpdesk -o yaml
helm status helpdesk -n helpdesk
helm get values helpdesk -n helpdesk
```

Include the chart version, Kubernetes version and distribution, cloud or datacenter environment, sanitized values file, relevant events, and pod logs.

| Channel                             | Use when                                      |
| ----------------------------------- | --------------------------------------------- |
| DuploCloud Slack #si-support        | First-line support; most issues resolved here |
| DuploCloud support portal           | Formal ticket with SLA tracking               |
| GitHub Issues (duplocloud/helpdesk) | Bug reports with reproduction steps           |

***

## 7. Uninstall

```bash
helm uninstall helpdesk --namespace helpdesk
```

**What uninstall leaves behind:**

* Secrets with `helm.sh/resource-policy: keep` (JWT shared secret, encryption key)
* The backup PVC (retained by the `Retain` reclaim policy)

Clean up manually if performing a full teardown. Preserve the `encryptionMasterKey` secret if you intend to restore data later.
