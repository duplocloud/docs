---
description: >-
  Reference for the Helm chart values used to configure a DuploCloud AI HelpDesk
  installation — application settings, authentication, storage, ingress, and
  optional integrations.
---

# Helm Chart Configuration

DuploCloud AI HelpDesk is deployed into a Kubernetes cluster using a Helm chart. This page documents the chart **values** — the configuration options that control the application's domain, authentication, storage, ingress, components, and integrations.

For the cloud infrastructure each environment requires, see the [Installation overview](./) and the per-cloud guides for [AWS](aws-installation.md), [Azure](azure-installation.md), and [GCP](gcp-installation.md).

***

## Prerequisites

The chart is cloud-agnostic and runs on any Kubernetes cluster — managed (EKS, AKS, GKE) or self-managed (on-premises, bare-metal, or VM-based). Before installing, the target cluster must provide the following.

### Cluster access

A Kubernetes cluster and a kubeconfig with permission to install into a namespace. Two worker nodes with roughly 2 vCPU and 8 GiB of memory each is sufficient for a standard deployment.

### Storage

Two kinds of persistent storage are required:

| Need                    | Used by                                    | Requirement                                                                                 |
| ----------------------- | ------------------------------------------ | ------------------------------------------------------------------------------------------- |
| **ReadWriteMany (RWX)** | Backend and Duplo Agent shared file volume | A StorageClass that provisions RWX volumes — NFS, AWS EFS, GCP Filestore, Azure Files, etc. |
| **ReadWriteOnce (RWO)** | MongoDB data volume                        | Any RWO StorageClass.                                                                       |
| **ReadWriteOnce (RWO)** | MongoDB backup volume                      | Any RWO StorageClass.                                                                       |

The RWX requirement can be satisfied two ways:

* Provide a StorageClass that dynamically provisions RWX volumes and set `backend.persistence.storageClass`.
* Pre-create an RWX PersistentVolumeClaim and reference it with `backend.persistence.existingClaim` — the chart then skips PVC creation.

{% hint style="info" %}
If the cluster has no managed RWX StorageClass, the chart can deploy a bundled in-cluster NFS server provisioner — set `nfs-server.enabled=true`. See [Persistent storage](helm-chart-configuration.md#persistent-storage).
{% endhint %}

### Ingress controller

An ingress controller must already be installed in the cluster — for example, the NGINX ingress controller. The chart creates `Ingress` resources but does **not** install a controller. Pass the controller's class via `ingress.className` (e.g. `nginx` or `alb`).

### DNS hostname

The hostname (FQDN) must be **decided** before installation — the chart uses it to create the host-based ingress routing rules and to build OAuth redirect URIs. The DNS record itself does not need to resolve yet; it is created after the ingress controller is assigned an address.

The deployment uses two hostnames:

* The main application URL — set in `config.authFrontendBaseUrl` (e.g. `https://ai-helpdesk.example.com`).
* The web terminal — set in `xterm.hostname` (e.g. `https://xterm.example.com`).

The typical order is:

1. Choose the hostnames and set them in the values file.
2. Install the chart — the ingress controller is assigned an address (IP or VIP).
3. Create DNS records pointing the chosen hostnames at that address.

On a private or on-premises cluster the records point at the ingress address on your LAN subnet — they do not need to be internet-routable.

### TLS certificate

A valid TLS certificate matching the application DNS name, terminated at the ingress controller (or an upstream load balancer).

{% hint style="warning" %}
HTTPS is mandatory — the platform cannot be used over plain HTTP. External login via OAuth/SSO providers (Okta, Google, Microsoft) requires HTTPS redirect URIs, so a valid certificate must be in place before users can sign in.
{% endhint %}

***

## How values are organized

Values are supplied through a values file. They fall into a few groups:

| Group                                           | Purpose                                                                                      |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `config`                                        | Non-sensitive application settings (domain, super-users, region) — rendered into a ConfigMap |
| `secrets`                                       | Sensitive settings (JWT secret, encryption key, SSO credentials) — rendered into a Secret    |
| `ingress` / `internalIngress`                   | External and internal HTTP routing                                                           |
| `backend`, `frontend`, `duploAgent`, `xterm`, … | Per-component deployment settings (replicas, resources, storage)                             |
| `mongodb`                                       | Embedded database and backups                                                                |
| `slackBackend`, `teamsBackend`                  | Optional chat integrations                                                                   |
| `bedrockSubscription`                           | AWS Bedrock model EULA acceptance                                                            |

***

## Required values

These must be provided for every installation regardless of cloud provider.

| Value                        | Description                                                                                                                                                       |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `config.authFrontendBaseUrl` | Public URL where the app is hosted, e.g. `https://ai-helpdesk.yourcompany.com`. Also used to build OAuth redirect URIs and as the host for the main ingress rule. |
| `config.authAllowedOrigins`  | Comma-separated list of origins allowed by CORS — typically the same value as `authFrontendBaseUrl`.                                                              |
| `config.authSuperUsers`      | Comma-separated list of email addresses granted super-admin access.                                                                                               |
| `secrets.jwtSharedSecret`    | Random secret used to sign internal JWTs. Generate with `openssl rand -base64 48`.                                                                                |
| `mongodb.auth.rootPassword`  | MongoDB root password (required when the embedded MongoDB is enabled).                                                                                            |

{% hint style="warning" %}
`secrets.encryptionMasterKey` is a 96-byte base64 master key used for field-level encryption. **Leave it empty and the chart auto-generates it on first install and reuses it on upgrades.** If you set it manually (`openssl rand -base64 96`), you must preserve the same value across all future upgrades or encrypted data becomes unreadable.
{% endhint %}

***

## Application configuration (`config`)

Non-sensitive settings rendered into a ConfigMap.

| Key                               | Default                              | Description                                                                                                       |
| --------------------------------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| `config.aspnetcoreEnvironment`    | `Production`                         | ASP.NET Core environment name.                                                                                    |
| `config.authFrontendBaseUrl`      | `""`                                 | Public base URL of the frontend. **Required.**                                                                    |
| `config.authAllowedOrigins`       | `""`                                 | CORS allowed origins. **Required.**                                                                               |
| `config.authSuperUsers`           | `""`                                 | Comma-separated super-admin emails. **Required.**                                                                 |
| `config.authCallbackPath`         | `/api/Account/ExternalLoginCallback` | Relative OAuth redirect path.                                                                                     |
| `config.mongoDbDatabaseName`      | `duplo-ai-helpdesk`                  | Database name the backend connects to.                                                                            |
| `config.infraRegion`              | `us-east-1`                          | Cloud region used for storage configuration.                                                                      |
| `config.agentBaseUrl`             | `""`                                 | Override the agent base URL. Defaults to the in-cluster `duplo-agent` service when empty.                         |
| `config.aiStudioIsMasterDisabled` | `true`                               | When `true`, disables the DuploCloud master-account integration.                                                  |
| `config.duploMasterUrl`           | `""`                                 | DuploCloud portal URL. Required only when `aiStudioIsMasterDisabled` is `false` (integrated mode).                |
| `config.azureBaseUrl`             | `""`                                 | Azure AI Foundry endpoint for Claude access via Azure, e.g. `https://<resource>.services.ai.azure.com/anthropic`. |

***

## Authentication and secrets (`secrets`)

Sensitive settings rendered into a Kubernetes Secret. Empty values are allowed — the secret is still created so individual keys can be patched later.

{% hint style="info" %}
To manage credentials outside the chart, set `secrets.existingSecret` to the name of a pre-existing Secret that already contains all required keys. The chart then references it directly instead of creating one.
{% endhint %}

| Key                               | Description                                                                                          |
| --------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `secrets.jwtSharedSecret`         | **Required.** Random secret for internal JWT signing.                                                |
| `secrets.encryptionMasterKey`     | 96-byte base64 master key for field-level encryption. Auto-generated when empty (see warning above). |
| `secrets.mongoDbConnectionString` | External MongoDB connection string. Used **only** when `mongodb.enabled=false`.                      |
| `secrets.existingSecret`          | Name of a pre-existing Secret to use instead of creating one.                                        |

### SSO / OAuth providers

Provide credentials for whichever identity providers you use.

{% tabs %}
{% tab title="Google" %}
| Key                          | Description                 |
| ---------------------------- | --------------------------- |
| `secrets.googleClientId`     | Google OAuth client ID.     |
| `secrets.googleClientSecret` | Google OAuth client secret. |
{% endtab %}

{% tab title="Microsoft" %}
| Key                             | Description                    |
| ------------------------------- | ------------------------------ |
| `secrets.microsoftClientId`     | Microsoft OAuth client ID.     |
| `secrets.microsoftClientSecret` | Microsoft OAuth client secret. |
| `secrets.microsoftTenantId`     | Microsoft Entra tenant ID.     |
{% endtab %}

{% tab title="Keycloak" %}
| Key                            | Description             |
| ------------------------------ | ----------------------- |
| `secrets.keycloakAuthority`    | Keycloak authority URL. |
| `secrets.keycloakHost`         | Keycloak host.          |
| `secrets.keycloakRealm`        | Keycloak realm.         |
| `secrets.keycloakClientId`     | Keycloak client ID.     |
| `secrets.keycloakClientSecret` | Keycloak client secret. |
{% endtab %}

{% tab title="Okta" %}
| Key                        | Description         |
| -------------------------- | ------------------- |
| `secrets.oktaDomain`       | Okta domain.        |
| `secrets.oktaClientId`     | Okta client ID.     |
| `secrets.oktaClientSecret` | Okta client secret. |
{% endtab %}
{% endtabs %}

### Azure AI Foundry credentials

Used when the AI agent talks to Claude through Azure AI Foundry.

| Key                             | Description                                                                                             |
| ------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `secrets.azureClientId`         | Managed-identity client ID (user-assigned MI auth). Leave empty for system-assigned MI or API-key auth. |
| `secrets.azureApiKey`           | Azure AI Foundry API key (API-key auth). Leave empty when using managed identity.                       |
| `secrets.authProvisioningToken` | Provisioning token.                                                                                     |

***

## Ingress

The chart configures two ingress resources: a public one for the UI and API, and an internal one for components that should not be reachable from the internet.

### Public ingress (`ingress`)

| Key                   | Default                                             | Description                                                                                                                                                                                                                       |
| --------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ingress.enabled`     | `true`                                              | Create the public ingress.                                                                                                                                                                                                        |
| `ingress.className`   | `alb`                                               | IngressClass — `alb` (AWS), `nginx`, or `azure-application-gateway`.                                                                                                                                                              |
| `ingress.annotations` | `{ alb.ingress.kubernetes.io/ssl-redirect: '443' }` | Annotations for the ingress controller (TLS cert ARN, scheme, subnets, etc.).                                                                                                                                                     |
| `ingress.tls`         | `[]`                                                | TLS blocks. Leave empty when TLS is terminated at the load balancer (e.g. ALB + ACM).                                                                                                                                             |
| `ingress.paths`       | _(preset)_                                          | Path-to-service routing. The host is derived from `config.authFrontendBaseUrl`. `/api`, `/swagger`, and auth paths route to the backend; `/mcp` and `/core-mcp` route to the MCP servers; everything else routes to the frontend. |

{% hint style="info" %}
**Using the NGINX ingress controller?** The following annotations are required — `ssl-redirect` forces HTTPS, and the larger proxy buffers are needed to handle the application's auth response headers. Set `tls.secretName` to the Secret holding your certificate, and list every hostname the certificate covers.

```yaml
ingress:
  enabled: true
  className: nginx
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    nginx.ingress.kubernetes.io/proxy-buffer-size: "128k"
    nginx.ingress.kubernetes.io/proxy-buffers-number: "4"
  tls:
    - secretName: helpdesk-tls
      hosts:
        - duplo.example.net
        - xterm.example.net
```
{% endhint %}

### Internal ingress (`internalIngress`)

| Key                           | Default                                 | Description                                                    |
| ----------------------------- | --------------------------------------- | -------------------------------------------------------------- |
| `internalIngress.enabled`     | `true`                                  | Create the internal ingress (routes to the Duplo Agent).       |
| `internalIngress.className`   | `alb`                                   | IngressClass for internal routing.                             |
| `internalIngress.hostname`    | `""`                                    | Optional host for host-based routing. Empty matches all hosts. |
| `internalIngress.annotations` | `{ scheme: internal, target-type: ip }` | Annotations marking the load balancer internal-only.           |

{% hint style="info" %}
**Ingress class and annotations are cloud-specific.** AWS uses `alb` with ALB annotations; GCP and Azure typically use `nginx` with cert-manager, or Azure Application Gateway. See the [per-cloud installation guides](./) for complete annotation examples.
{% endhint %}

***

## Persistent storage

The backend and the Duplo Agent share a `ReadWriteMany` (RWX) file volume for tickets, projects, skills, and agent working directories. The right `storageClass` depends on your infrastructure setup.

{% tabs %}
{% tab title="AWS (EFS)" %}
```yaml
backend:
  persistence:
    enabled: true
    storageClass: efs-sc        # backed by the EFS CSI driver (pre-created)
    accessModes: [ReadWriteMany]
    size: 10Gi
    mountPath: /data/ai-helpdesk
```
{% endtab %}

{% tab title="GCP (Filestore)" %}
```yaml
backend:
  persistence:
    enabled: true
    storageClass: filestore-rwx  # backed by the Filestore CSI driver (pre-created)
    accessModes: [ReadWriteMany]
    size: 1Ti                    # Filestore Basic tier minimum
    mountPath: /data/ai-helpdesk
```
{% endtab %}

{% tab title="Azure (Azure Files)" %}
```yaml
backend:
  persistence:
    enabled: true
    storageClass: azurefile-csi-nfs  # Azure Files NFS StorageClass (pre-created)
    accessModes: [ReadWriteMany]
    size: 100Gi
    mountPath: /data/ai-helpdesk
```
{% endtab %}

{% tab title="In-cluster NFS" %}
When no managed RWX StorageClass is available, enable the bundled NFS server provisioner. It creates a StorageClass that the backend and agent PVCs use automatically.

```yaml
nfs-server:
  enabled: true
  storageClass:
    name: nfs
```
{% endtab %}
{% endtabs %}

### Backend persistence (`backend.persistence`)

| Key                                 | Default             | Description                                       |
| ----------------------------------- | ------------------- | ------------------------------------------------- |
| `backend.persistence.enabled`       | `true`              | Mount a shared volume into the backend.           |
| `backend.persistence.existingClaim` | `""`                | Use a pre-existing PVC instead of creating one.   |
| `backend.persistence.storageClass`  | `""`                | RWX StorageClass. Empty uses the cluster default. |
| `backend.persistence.accessModes`   | `[ReadWriteMany]`   | RWX is required when `replicaCount > 1`.          |
| `backend.persistence.size`          | `10Gi`              | Requested storage size.                           |
| `backend.persistence.mountPath`     | `/data/ai-helpdesk` | Mount path inside the backend container.          |
| `backend.persistence.subPath`       | `""`                | Optional sub-path within the volume.              |

The **Duplo Agent** uses the same shared volume through `duploAgent.persistence`, with sub-path mounts for `tickets`, `projects`, `skills`, `agents`, and `workspaces`.

***

## Database (`mongodb`)

By default the chart deploys an embedded Bitnami MongoDB with daily backups. To use an external MongoDB instead, set `mongodb.enabled=false` and provide `secrets.mongoDbConnectionString`.

| Key                                | Default    | Description                                                       |
| ---------------------------------- | ---------- | ----------------------------------------------------------------- |
| `mongodb.enabled`                  | `true`     | Deploy the embedded MongoDB.                                      |
| `mongodb.auth.rootUser`            | `authuser` | MongoDB root username.                                            |
| `mongodb.auth.rootPassword`        | `""`       | **Required** when embedded. MongoDB root password.                |
| `mongodb.persistence.enabled`      | `true`     | Persist MongoDB data on a PVC.                                    |
| `mongodb.persistence.size`         | `8Gi`      | MongoDB PVC size.                                                 |
| `mongodb.persistence.storageClass` | `""`       | StorageClass for the MongoDB PVC. Empty uses the cluster default. |
| `mongodb.useStatefulSet`           | `false`    | Run MongoDB as a StatefulSet instead of a Deployment.             |

### Backups (`mongodb.backup`)

| Key                                             | Default     | Description                                                |
| ----------------------------------------------- | ----------- | ---------------------------------------------------------- |
| `mongodb.backup.enabled`                        | `true`      | Enable the `mongodump` backup CronJob.                     |
| `mongodb.backup.cronjob.schedule`               | `0 0 * * *` | Cron schedule for backups.                                 |
| `mongodb.backup.cronjob.storage.size`           | `25Gi`      | Disk reserved for backup dumps.                            |
| `mongodb.backup.cronjob.storage.storageClass`   | `""`        | StorageClass for the backup PVC.                           |
| `mongodb.backup.cronjob.storage.resourcePolicy` | `""`        | Set to `keep` to preserve the backup PVC on `helm delete`. |

***

## AI Agent model configuration (`duploAgent`)

The Duplo Agent runs Claude. It can reach Claude through **AWS Bedrock**, **Azure AI Foundry**, or the **Anthropic API directly**. The `CLAUDE_MODEL` ID format **depends on which provider you use**, and using the wrong format causes authentication failures.

{% hint style="danger" %}
**`CLAUDE_MODEL` format differs by provider:**

* **AWS Bedrock:** `us.anthropic.claude-sonnet-4-6`
* **Azure AI Foundry:** `claude-sonnet-4-6`
* **Anthropic API (direct):** `claude-sonnet-4-6`

Using the Bedrock format with Azure or the Anthropic API (or vice versa) will fail authentication.
{% endhint %}

Agent runtime settings are passed through `duploAgent.extraEnv`. Commonly used variables:

| Variable               | Example                                              | Description                                                                              |
| ---------------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `CLAUDE_MODEL`         | `claude-sonnet-4-6`                                  | Claude model ID (provider-specific format — see above).                                  |
| `ANTHROPIC_API_KEY`    | `sk-ant-api03-…`                                     | Anthropic API key. Set this to call the Anthropic API directly instead of Bedrock/Azure. |
| `AZURE_BASE_URL`       | `https://<resource>.services.ai.azure.com/anthropic` | Azure AI Foundry endpoint.                                                               |
| `AZURE_CLIENT_ID`      | `xxxxxxxx-…`                                         | User-assigned managed identity client ID (omit for system-assigned MI).                  |
| `LOG_LEVEL`            | `INFO`                                               | `DEBUG`, `INFO`, `WARNING`, or `ERROR`.                                                  |
| `CCA_MAX_TURNS`        | `20`                                                 | Maximum conversation turns per session.                                                  |
| `CCA_MAX_BUDGET_USD`   | `5.00`                                               | Maximum spend per session.                                                               |
| `CCA_EXTRA_READ_PATHS` | `/data/skills`                                       | Extra readable paths for the agent sandbox.                                              |

### Using the Anthropic API directly

To bypass Bedrock and Azure and call the Anthropic API directly, the agent deployment needs just two environment variables — an Anthropic API key and the model ID in the **non-prefixed** format:

```yaml
duploAgent:
  extraEnv:
    - name: ANTHROPIC_API_KEY
      value: sk-ant-api03-...        # your Anthropic API key
    - name: CLAUDE_MODEL
      value: claude-sonnet-4-6       # direct-API format (no "us.anthropic." prefix)
```

{% hint style="warning" %}
`ANTHROPIC_API_KEY` is sensitive. Prefer storing it in the chart Secret and referencing it with `valueFrom.secretKeyRef` rather than placing the literal key in `extraEnv`:

```yaml
duploAgent:
  extraEnv:
    - name: ANTHROPIC_API_KEY
      valueFrom:
        secretKeyRef:
          name: helpdesk-secrets    # or your custom secret name
          key: anthropicApiKey
    - name: CLAUDE_MODEL
      value: claude-sonnet-4-6
```
{% endhint %}

When `ANTHROPIC_API_KEY` is set, do **not** also set `AZURE_BASE_URL` or rely on Bedrock IRSA — the direct API key takes precedence and the model ID must use the non-prefixed format (`claude-sonnet-4-6`).

{% hint style="info" %}
The agent runs commands inside a `bubblewrap` sandbox that needs the `SYS_ADMIN` (and reserved `NET_ADMIN`) Linux capabilities. These are set by default in `duploAgent.securityContext` — do not remove them or sandboxed command execution will break.
{% endhint %}

<details>

<summary>Azure AI Foundry: managed identity vs. API key</summary>

**Managed identity (preferred on Azure):** set `AZURE_BASE_URL` and, for a user-assigned identity, `AZURE_CLIENT_ID`. No secrets to rotate — the SDK acquires and refreshes tokens automatically.

**API key:** set `AZURE_BASE_URL` and supply the key via `secrets.azureApiKey` (referenced as an env var) rather than hardcoding it in `extraEnv`.

In both cases set `CLAUDE_MODEL` to the Azure format (`claude-<model-name>`).

</details>

***

## AWS Bedrock model subscription (`bedrockSubscription`)

On AWS, a post-install Helm hook Job accepts the Bedrock model EULAs so the agent can invoke the models. It runs after the application pods start and does not block them.

| Key                                              | Default         | Description                                                                                 |
| ------------------------------------------------ | --------------- | ------------------------------------------------------------------------------------------- |
| `bedrockSubscription.enabled`                    | `true`          | Run the EULA-acceptance Job.                                                                |
| `bedrockSubscription.models`                     | _(preset list)_ | Bedrock model IDs to accept EULAs for.                                                      |
| `bedrockSubscription.serviceAccount.irsaRoleArn` | `""`            | IRSA role ARN with `bedrock:*` permissions. In integrated mode this is the tenant role ARN. |
| `bedrockSubscription.ttlSecondsAfterFinished`    | `3600`          | Seconds before the finished Job is auto-deleted.                                            |

***

## Components

The chart deploys these components. Each can be sized and toggled independently; image repositories/tags are set by DuploCloud.

| Component           | Value prefix   | Default enabled | Description                                                        |
| ------------------- | -------------- | --------------- | ------------------------------------------------------------------ |
| Backend             | `backend`      | always          | ASP.NET Core API — tickets, projects, agent orchestration.         |
| Frontend            | `frontend`     | always          | nginx-served Angular web UI.                                       |
| Duplo Agent         | `duploAgent`   | `true`          | Claude-powered AI agent runtime.                                   |
| Web Terminal        | `xterm`        | `true`          | Browser-based terminal with an SSO-proxy sidecar.                  |
| HelpDesk MCP Server | `helpdeskMcp`  | `true`          | Model Context Protocol server for helpdesk tools.                  |
| Core MCP Server     | `coreMcp`      | `false`         | DuploCloud platform MCP server (requires `config.duploMasterUrl`). |
| Slack Backend       | `slackBackend` | `true`          | Slack integration.                                                 |
| Teams Backend       | `teamsBackend` | `false`         | Microsoft Teams integration.                                       |
| MongoDB             | `mongodb`      | `true`          | Embedded database.                                                 |

Common per-component keys: `replicaCount`, `resources.{requests,limits}.{cpu,memory}`, `nodeSelector`, `tolerations`, `affinity`, `podAnnotations`, and (for backend / duploAgent) `hpa.*` for autoscaling and `serviceAccount.irsaRoleArn` for cloud IAM.

{% hint style="info" %}
**Node placement.** On clusters where component pods must land on specific nodes (for example, a DuploCloud tenant), set the global `nodeSelector` (e.g. `{ kubernetes.io/os: linux, tenantname: <namespace> }`). Per-component `nodeSelector` values merge on top of the global one, with the component value winning.
{% endhint %}

***

## Chat integrations

### Slack (`slackBackend`)

| Key                                                       | Description                                               |
| --------------------------------------------------------- | --------------------------------------------------------- |
| `slackBackend.enabled`                                    | Enable the Slack backend.                                 |
| `slackBackend.env.helpdeskWorkspaceLabel`                 | Workspace label shown in the helpdesk UI.                 |
| `slackBackend.env.helpdeskDefaultWorkspace`               | Default workspace the Slack backend connects to.          |
| `slackBackend.env.helpdeskDefaultAgent`                   | Default agent for new sessions.                           |
| `slackBackend.env.helpdeskAllowedScopeIds`                | Comma-separated scope IDs the backend may access.         |
| `slackBackend.envFromSecret.data.SLACK_APP_TOKEN`         | Slack app-level token (`xapp-…`).                         |
| `slackBackend.envFromSecret.data.SLACK_BOT_TOKEN`         | Slack bot OAuth token (`xoxb-…`).                         |
| `slackBackend.envFromSecret.data.DUPLO_SLACK_APP_PORTALS` | List of `{ duplo_host, duplo_token }` portal credentials. |

### Microsoft Teams (`teamsBackend`)

| Key                                                       | Description                                                              |
| --------------------------------------------------------- | ------------------------------------------------------------------------ |
| `teamsBackend.enabled`                                    | Enable the Teams backend (disabled by default).                          |
| `teamsBackend.hostname`                                   | Host for ingress routing — must match `teamsPublicBaseUrl`.              |
| `teamsBackend.env.teamsPublicBaseUrl`                     | Public base URL of the Teams bot.                                        |
| `teamsBackend.envFromSecret.data.MS_APP_ID`               | Microsoft App ID from the Azure Bot resource.                            |
| `teamsBackend.envFromSecret.data.MS_APP_PASSWORD`         | Microsoft App password (client secret).                                  |
| `teamsBackend.envFromSecret.data.MS_APP_TENANT_ID`        | Customer's Entra tenant ID.                                              |
| `teamsBackend.envFromSecret.data.TEAMS_MODAL_SECRET`      | 32-byte hex secret for Task Module JWT signing (`openssl rand -hex 32`). |
| `teamsBackend.envFromSecret.data.DUPLO_SLACK_APP_PORTALS` | List of `{ duplo_host, duplo_token }` portal credentials.                |

{% hint style="info" %}
For both integrations, the chart creates the credential Secret when `envFromSecret.create=true` (default). To manage the Secret yourself, set `create: false` and provide an existing Secret with all required keys in the same namespace.
{% endhint %}
