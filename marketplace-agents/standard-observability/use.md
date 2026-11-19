---
description: Step-by-step walkthroughs of the main things Standard Observability does.
---

# Use

## Create a stack

1. Open **Observability > Standard Observability** and select **Create Observability Stack** (or add a stack from the list).
2. **Basics**: enter a **Stack Name** (it cannot be changed later). Choose a **Provisioning Mode**:
   - **Use the DevOps extension**: builds on an Environment and Resource Group in the workspace, plus a Network Baseline and Kubernetes cluster when a new Resource Group is created.
   - **Standalone (AWS and Kubernetes scopes only)**: choose the AWS scope, the Kubernetes scope, the **Region** and the **EKS Cluster**. No Environment or Resource Group is created or changed. FluxCD must already be installed.
3. **Cluster Add-ons**: the wizard reads the cluster and shows which of FluxCD, the AWS Load Balancer Controller, the cluster autoscaler and external-dns are running. Install any required one that is missing, then select **Re-check**. The stack does not install these add-ons.
4. **Node Pool**: select **Create New Node Pool** (set instance type, **Min**, **Desired**, **Max** and **Disk (GB)**), or **Use Existing Nodes** and enter the labels they carry.
5. **Log Storage**: select **Create Automatically** or **Use Existing Bucket**, and set **Retention (hours)** (default 8760, one year). You can enable an internal Loki endpoint for other clusters to send logs to, with a hostname prefix.
6. **Monitoring**: turn Prometheus on or off. Set **Retention (days)** (default 90), **Disk size (GB)** (default 100) and **Retention size (GB)** (default 90). The size limit means a busy cluster drops its oldest data instead of filling the disk. You can enable an internal Prometheus endpoint (remote write).
7. **Grafana**: set the local **Admin Password** and confirm it. It needs at least 8 characters with an upper-case letter, a lower-case letter, a digit and a special character. **Portal URL for SSO** defaults to the portal you are using.
8. **Endpoints**: choose the **Certificate ARN**, the **Grafana Hostname Prefix** and the **DNS Suffix**. Choose **I will create it** or **Create it automatically (external-dns)** for the DNS record.
9. **Review & Submit**: the wizard lists steps that still have problems, with links to fix them. Select the submit button to start provisioning.

<!-- VERIFY: field names are taken from the wizard source, not a live run. Screenshots SO-03 to SO-10. Confirm the final button label on the Review step and whether the wizard is still the same after the planned simplification sub-ticket. -->

## Follow provisioning

Select **Track Provisioning** in the list menu, or open the stack. The page shows each phase and its state: not started, in progress, complete, skipped or failed. Typical phases are AWS preflight, cluster components, observability node pool, node networking, log storage, S3 VPC endpoint, Helm repositories, Helm releases, endpoints and verification. Standalone mode adds cluster access, prerequisites, namespace and workload identity phases.

A full run can take a while: the platform allows up to 45 minutes for provisioning and 15 minutes for teardown.

<!-- VERIFY: the 2700 s and 900 s limits come from the extension manifest. Confirm they are what customers should be told. Screenshot SO-11. -->

## Create the DNS record (if you chose "I will create it")

1. When the stack stops with status **Blocked**, open it. The page shows **Action required - create this DNS record** and the exact record.
2. Create the record in your DNS zone, then select **I've created it - re-check**.
3. If the record resolves but the load balancer is not answering yet, wait a minute and select **Re-check** again.

With **Create it automatically (external-dns)** no action is needed here, provided external-dns on the cluster has permission for the zone.

<!-- VERIFY: button wording on the page uses a typographic dash; confirm exact text. Screenshot SO-13. -->

## Register the Grafana scope

When Grafana is reachable but no scope is registered, the page shows **Action required - register the Grafana scope**. A scope lets agents and other resources get credentials for this Grafana.

- **Administrators**: select **Create Grafana scope**. It creates a provider and a scope named `grafana-<stack name>` and attaches the scope to the workspace.
- **Other users**: pick a scope an administrator already attached to the workspace under **Associate an existing scope**, then select **Save**.

You can change the scope later with **Change**.

<!-- VERIFY: sub-ticket exists for the Grafana scope test and the non-admin path. Confirm in QA that a non-admin sees the 403 message and the association path works. Screenshot SO-14, SO-15. -->

## Open your dashboards

Open **Observability > Standard Observability**. If a stack is complete, you land on the dashboards page. Pick a stack and a dashboard, and Grafana opens in a frame (kiosk mode is on by default; a button opens it in its own tab). Dashboards include the Kubernetes compute, node, pod, persistent volume, networking, API server, CoreDNS and Prometheus overview dashboards, plus **Explore** for logs (Loki) and metrics (Prometheus). Stacks without monitoring show only Explore and the dashboard list.

<!-- VERIFY: dashboard names come from the default favourites in the code. Confirm they match the shipped chart version. Screenshot SO-16. -->

## Curate favourites

On the stack page, the **Favourites** panel controls what the dashboard picker offers. Add an entry with a name and a path inside Grafana that starts with `/` (for example `/explore`), star one to open first, edit or remove entries, and drag to reorder (confirm to save the order). Changes do not re-run provisioning.

## Send logs and metrics from other clusters

If you enabled the internal Loki or Prometheus endpoint, the stack's result page shows the push URLs (`https://<host>/loki/api/v1/push` and `https://<host>/api/v1/write`). These load balancers are internal, so only clients inside the VPC or peered networks can reach them. Collectors in the same cluster use Loki's in-cluster address.

<!-- VERIFY: this README mentions a collector-only mode for other clusters as a future item (M3). Confirm that customers install the collectors in other clusters themselves. -->

## Edit a stack

Select **Edit** from the list menu. Saving re-runs provisioning with the new settings. The name, mode, cluster, environment, resource group and namespace are fixed once created.

## Remove a stack

1. Select **Deprovision** from the list or stack menu. A summary shows what is removed and what is kept. Confirm twice.
2. The agent first prints a preview and waits for your written confirmation in the ticket chat before it removes anything.

Kept after teardown: the log bucket, the S3 VPC endpoint, the namespace and the Prometheus volume (metric history), shared cluster add-ons, and in standalone mode the cluster's OIDC provider and security group rules. DNS records created by external-dns are removed when the ingress goes; records you made yourself stay.

**Delete** removes only the stack record from DuploCloud and does not remove cloud resources. Use Deprovision first.

<!-- VERIFY: "Delete removes only the record" is inferred from the confirmation text "Delete from the database". Confirm. Screenshot SO-17. -->
