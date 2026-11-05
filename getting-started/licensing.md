---
description: >-
  The licenses DuploCloud AI Suite uses, how to get a trial or an environment
  license, how to apply one, and what to do when a license expires or fails.
---

# Licensing

Every DuploCloud AI Suite deployment needs a license issued by DuploCloud, whether it is the DevKit on your laptop or a portal running in your own cloud. A license is a signed token that says who or what it belongs to and carries the limits (users, workspaces, providers, agents, and tickets per month) the platform enforces.

This page covers which license you need, how to get one, the ways to apply it, and how to read and troubleshoot the **License** tab under Access Control.

***

## Which license do I need?

| License | What it is for | Who issues it | What ties it to you |
| --- | --- | --- | --- |
| **Trial** | Running the DevKit locally to build and try agents | Requested automatically by the DevKit the first time you run it | Your email address. It is not tied to a host. |
| **Free-tier environment** | Running your own portal in your own cloud account, without a sales conversation | Created by you in the [DuploCloud Console](https://console.duplocloud.com), or automatically by Cloud Deploys | The portal's hostname, for example `helpdesk.example.com` |
| **Customer** | Production deployments for DuploCloud customers | DuploCloud, through your account team | The portal's hostname (one license per environment) |

Trial and free-tier licenses have limits on users, workspaces, providers and agents. The exact limits are set by DuploCloud and can change, so check the License tab (or your license in the Console) for the values that apply to you. A free-tier company can have one cloud environment. Customer licenses are normally unlimited.

***

## Get a trial license through the DevKit

You don't request a trial license by hand. The first time you run the DevKit (see [Install the DevKit](install-the-devkit.md)), it asks for an admin email address and requests a trial for it:

1. DuploCloud emails that address a verification link. Use an address you can read right away. Work and personal addresses are fine, but privacy-relay and disposable domains are refused.
2. Click the link. The DevKit is waiting for it, picks up the license, and stores the token in its configuration. You don't need to copy anything.
3. The local studio starts with the trial license in force.

Keep these rules in mind:

* **One license per email address.** DuploCloud never issues a second trial for the same address, so the DevKit is built to reuse the license it already has.
* **Recovery, not re-issue.** If you re-clone the DevKit or clear its configuration, running it again with the same address recovers your existing license: you get a confirmation email, and clicking it releases the same license (same expiry) to the new copy.
* **Already have a token?** Skip the email flow with `./run.sh --license <jwt>`. Pass the bare token with no quotes or line breaks.
* **Keep the token safe.** It is a credential, and because it is never re-issued, losing it means going through recovery.

The variables the DevKit uses and every message it can print are documented in the DevKit repository: see [Licensing in the configuration reference](https://github.com/duplocloud/devkit/blob/main/docs/configuration.md#licensing) and [Licensing troubleshooting](https://github.com/duplocloud/devkit/blob/main/docs/troubleshooting.md#licensing).

***

## Get an environment license for your own portal

A portal running in your own cloud account needs an **environment license** bound to the hostname it runs on. Your DevKit trial license will not work there, because it is tied to your email address, not a host.

You can get an environment license in two ways:

* **From the Console.** Sign in to the [DuploCloud Console](https://console.duplocloud.com), open **Environments**, and click **Add environment**. Enter a name and the URL your portal will run at. On the free tier the environment and its license are created together; open the environment's license to copy the token. Then supply it to your portal (see [Ways to apply a license](#ways-to-apply-a-license)).
* **Automatically, with Cloud Deploys.** When you deploy your portal from the DevKit with Cloud Deploys, it registers the environment with the Console for you, using your DevKit license as proof of who you are, and installs the environment license into the new portal. See [Deploy Your Portal to Your Cloud](installation/README.md).

{% hint style="info" %}
Cloud Deploys is in preview.
{% endhint %}

The hostname is locked once a license is issued for it. If you need to move your portal to a different URL, contact DuploCloud for a re-issued license.

If you are a DuploCloud customer, your account team issues environment licenses for your deployments. DuploCloud can also deploy the portal for a customer on a case-by-case basis; ask your account team.

***

## How licensing works

* **Issued by DuploCloud.** Licenses are minted by the DuploCloud Console and signed with a private key that never leaves DuploCloud. The platform verifies the signature against an embedded public key, so a token cannot be forged or edited.
* **Bound to one deployment or one person.** A DevKit trial license is bound to the email address it was issued for. An environment license carries the hostname of the deployment it was issued for (for example `helpdesk.example.com`). The platform compares that host against its own public URL (`config.authFrontendBaseUrl`) and refuses a license issued for a different host. If you move the deployment to a new URL, request a new license.
* **Carries entitlements.** The token sets the maximum number of users, workspaces, providers, agents, and tickets per month. A value of unlimited is the norm for customer licenses. Entitlements can only be changed by DuploCloud re-issuing the token.
* **Online or offline.** By default a license checks in with the DuploCloud Console (`https://console.duplocloud.com`) at startup, when applied, and every 6 hours afterwards, which allows DuploCloud to revoke a license or deliver a re-issued one. If the Console is unreachable, the license stays in force for a 72-hour grace period measured from the last successful check-in. A license issued with offline verification never contacts the Console and is bounded only by its expiry date — this is the form used for air-gapped installs.

{% hint style="warning" %}
**Without a valid license, the platform starts but refuses every create.** Users can sign in and the License tab remains reachable so an administrator can apply a token, but creating users, workspaces, providers, agents, or tickets is blocked until a valid license is in force. The reason is shown on the License tab and in the backend startup log.
{% endhint %}

***

## Ways to apply a license

The DevKit stores its trial license for you (see above). For a portal you run yourself, there are two ways to supply the license:

| Method                     | When to use                                                                    | How                                                                          |
| -------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| **Helm values** (install)  | New installs, GitOps-managed deployments, and anywhere the token should be part of the deployed configuration | Set `secrets.licensingToken` in `values.yaml` before `helm install`          |
| **License page** (manual)  | Applying a license after install, replacing a lapsed or re-issued license, recovering from a failed license without a redeploy | **AI Admin → Access Control → License → Apply New License** (steps below)    |

Both methods result in the same thing: a verified license persisted in the platform database and in force immediately. A license applied from the License page survives restarts and upgrades. When more than one token has been supplied, the **most recently issued** one wins — a token older than the one already installed is refused.

### Option 1 — Helm values

Add the token to the `secrets` block of your values file:

```yaml
secrets:
  licensingToken: "<LICENSE_TOKEN>"
```

Then install or upgrade the release:

```bash
helm upgrade --install helpdesk oci://quay.io/duplocloud/helpdesk \
  --version <VERSION> \
  --namespace helpdesk \
  --values values.yaml
```

If you manage secrets outside the chart with `secrets.existingSecret`, the chart ignores `secrets.licensingToken`; your Secret must carry the token under the key `Licensing__Token` instead.

{% hint style="info" %}
Treat the license token like any other credential. Keep it out of source control, and prefer an external secret manager (Vault, External Secrets Operator, Sealed Secrets) for production.
{% endhint %}

### Option 2 — Apply a license from the License page

Use this when the deployment is already running — for example when the Helm values did not include a token, the token has lapsed, or DuploCloud has re-issued a license with new entitlements. No restart is required.

#### Prerequisites

* Administrator access to the DuploCloud AI Suite
* The license token issued by DuploCloud for **this deployment's hostname**

#### Step 1 — Navigate to Access Control → License

Go to **AI Admin → Access Control** in the left-hand navigation and click the **License** tab. The page shows the installed license (if any) at the top and the entitlement limits in the table below.

![Step 1 — License tab](../.gitbook/assets/license-step-01-license-tab.png)

#### Step 2 — Click "Apply New License"

Click the **Apply New License** button above the limits table. The **Apply New License** dialog opens with a single **License Token** field.

![Step 2 — Apply New License dialog](../.gitbook/assets/license-step-02-apply-dialog.png)

#### Step 3 — Paste the token and click "Apply"

Paste the complete token exactly as DuploCloud issued it, then click **Apply**. Leading and trailing whitespace is trimmed automatically, but the token must otherwise be unmodified.

The token is verified **before** anything is saved. If verification fails, the dialog shows the reason and the license already installed (if any) is left untouched. If it succeeds, a **License Applied** confirmation appears, the dialog closes, and the license cards and limits table refresh to show the new license.

{% hint style="success" %}
A verified license takes effect immediately. Creates that were blocked are allowed as soon as the dialog closes — no restart or redeploy is needed.
{% endhint %}

***

## Reading the License tab

The cards across the top summarize the installed license:

| Card                              | Meaning                                                                                                                                           |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Licensed For** / **License Holder** | The deployment hostname the license is bound to, or, for a user license, the licensee's email address                                        |
| **Kind**                          | `environment` for a host-bound license; otherwise the license kind, such as `trial` or `customer`                                                 |
| **Status**                        | `Active` — in force; `Lapsed` — installed but no longer valid; `Not Installed` — no license has been supplied                                   |
| **Expires**                       | The expiry date, or `Never` for a perpetual license. The issue date is shown underneath.                                                        |
| **Console**                       | Shown only for a Console-managed (online) license: the last and next scheduled check-in with the DuploCloud Console                             |

The table below the cards lists each licensed dimension:

| Column          | Meaning                                                                                                                           |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Dimension**   | What is being limited (for example Users, Workspaces), with the token claim name underneath                                       |
| **In Use**      | How many currently exist                                                                                                          |
| **Limit**       | The cap from the license, or `Unlimited`                                                                                          |
| **Remaining**   | Headroom under the cap                                                                                                            |
| **Enforcement** | `Enforced` — the cap is being applied; `Blocked — No Valid License` — every create in this dimension is refused until a valid license is applied; `Not Enforced` — this build applies no cap to the dimension |

The agent limit appears in the current release as the **Extensions** row, with the claim name `max_extensions`. A later release relabels it **Agents** (`max_agents`).

A banner above the table explains why rows are blocked when no valid license is in force, and a red alert appears if the DuploCloud Console has revoked the license.

***

## What happens when a license expires

An expired license does not stop the platform. Users can still sign in, and existing workspaces, agents and tickets keep working, but every create (users, workspaces, providers, agents, tickets) is refused until a valid license is applied. The License tab shows the status `Lapsed`.

* **DevKit trial:** the DevKit warns you from seven days before expiry and on every run afterwards, but keeps starting. Running it again cannot produce a new license, because the address already has one. To renew, contact **sales@duplocloud.net**. If you are given a new token, install it with `./run.sh --license <jwt>`.
* **Environment license:** request a renewed license from DuploCloud (or your account team), then apply it from the License page or through Helm values.

***

## Troubleshooting

| Symptom or reason                           | Cause                                                                                     | Fix                                                                                                      |
| ------------------------------------------- | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| Status `Not Installed`; all creates refused | No token was supplied in Helm values or applied from the License page                     | Apply the license from the License page, or set `secrets.licensingToken` and upgrade the release         |
| `HostMismatch`                              | The license was issued for a different hostname than `config.authFrontendBaseUrl`         | Apply the license issued for this environment. If the deployment URL changed, request a new license      |
| `Expired` / Status `Lapsed`                 | The license is past its expiry date                                                       | See [What happens when a license expires](#what-happens-when-a-license-expires)                         |
| Token "could not be verified" (`Malformed`, `InvalidSignature`, `InvalidIssuer`, `InvalidAudience`) | The pasted value is incomplete, altered, or was not issued by DuploCloud | Re-copy the whole token exactly as issued and apply again                                                |
| `OlderThanInstalled`                        | The token is not newer than the license already installed                                 | Nothing to do if the installed license is correct; otherwise request a re-issued token                   |
| `UnsupportedVersion`                        | The token was minted by a newer Console than this installation understands                | Upgrade the installation, then apply the token again                                                     |
| `ConsoleUnreachable`                        | The platform cannot reach `console.duplocloud.com` to verify an online license            | Allow outbound HTTPS to the Console. If the environment is air-gapped, request an offline license        |
| `ConsoleRefused` / revoked banner           | DuploCloud has revoked the license                                                        | Contact DuploCloud                                                                                       |
| Applied from the page, but Helm shows an older token | A License-page apply is persisted in the database and takes precedence over an older Helm value | Update `secrets.licensingToken` to the current token so the two stay in sync                        |

For problems with the DevKit's trial license (the verification email, a mistyped address, an already registered address), see [Licensing troubleshooting](https://github.com/duplocloud/devkit/blob/main/docs/troubleshooting.md#licensing) in the DevKit repository.

Licensing as an install prerequisite, and how to supply the token through Helm values, is covered in the [Systems Integrator Installation Guide](installation/systems-integrator-installation-guide.md#id-1.12-license-token).
