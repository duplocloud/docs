---
description: Common problems with Standard Observability and how to fix them.
---

# Troubleshooting and FAQ

To run provisioning again after you fix a cause, open the stack, select **Edit** and save. Each phase finds what already exists and carries on from there.

## In the wizard

| What you see | What it means | What to do |
| --- | --- | --- |
| **Next** stays disabled on **Cluster Add-ons** | FluxCD or the AWS Load Balancer Controller isn't running on the cluster. | Install it, then select **Re-check**. |
| "external-dns is not running. You can continue…" | DNS records won't be created for you. | Continue and choose **I will create it** on Endpoints, or install external-dns. |
| No clusters in the **EKS Cluster** list | The Kubernetes scope's cluster isn't in the chosen region, or the AWS scope can't list clusters. | Check the region and the Kubernetes scope. You can type the cluster name by hand. |
| No certificates in **Certificate ARN** | There's no issued ACM certificate in the cluster's region, or the AWS scope can't list them. | Issue a certificate in that region, or select **Enter an ARN manually…**. |
| "This certificate does not cover…" | The certificate doesn't match the Grafana hostname, so browsers will reject it. | Choose a certificate that covers the hostname, or change the prefix or suffix. |
| "You cannot use the selected scope here" | The scope isn't attached to this workspace, or isn't granted to you. | Ask an administrator to attach the scope or grant it to you. |
| "Too many …, wait Ns and try again." | The wizard's live lookups are rate-limited. | Wait the time shown and try again. |
| Admin password rejected | It needs at least 8 characters with an upper-case letter, a lower-case letter, a digit and a special character. | Choose a stronger password. |

## While provisioning

| What you see | What it means | What to do |
| --- | --- | --- |
| **Blocked**: "Action required — create this DNS record" | You chose **I will create it**, and Grafana is unreachable until the record exists. | Create the record shown, then select **I've created it — re-check**. |
| **Blocked**, and the record resolves but Grafana doesn't answer | The load balancer may still be starting. | Wait a minute, then select **Re-check**. |
| **Blocked**: "the Grafana scope is not registered" | Grafana is reachable, but registering it as a provider and scope didn't go through. | Select **Re-check**. If it keeps failing, ask an administrator to check provider and scope permissions. |
| Fails early on the S3 VPC endpoint | The AWS scope's role can't read or create the endpoint. Nothing was created. | Give the role the EC2 permissions in [Permissions and Safety](permissions-and-safety.md#aws-permissions), then edit and save. |
| Fails on node networking, listing rules | The role can't add the security group rules the node pool needs. | Grant `ec2:AuthorizeSecurityGroupIngress`, or add the listed rules yourself. Don't widen them. |
| Fails: another active Prometheus Operator | Two cluster-wide operators would fight over the same objects. | Remove or pause the other operator, or turn monitoring off. |
| Fails: no usable StorageClass | The cluster has no StorageClass the stack can use. | Create a StorageClass, ideally marked default. |
| Stops, naming an existing object | An object with the same name exists in the namespace and wasn't created by this stack. | Rename or remove your object, or use another namespace. |
| A notice that the namespace already exists | The stack is using a namespace it didn't create. | No action. The stack never changes or deletes that namespace. |
| "Another run already in progress" | A run is already working on this stack. | Wait for it to finish. Nothing was changed. |
| An add-on shows as missing on the **Infrastructure** tab | The run found the add-on missing and carried on. | Install it if you need the feature it provides. |

## Signing in to Grafana

| What you see | What it means | What to do |
| --- | --- | --- |
| The browser stops at a "Redirecting to … duplo_auth" page | Your portal isn't allowed to sign people in to this Grafana yet. The agent normally adds this for you. | Ask an administrator to check **Settings > Workspace Settings** for a setting named `<stack name>-grafana`, labelled `sso-proxy`, with the Grafana address as its value. Add it if it's missing. |
| I need the local admin password | DuploCloud doesn't show it. It's kept only in the cluster. | Sign in through your portal instead, or read the `grafana-admin` Secret with the command on the stack's **Grafana** tab. |

## Dashboards

| What you see | What it means | What to do |
| --- | --- | --- |
| Only **Explore** and **All dashboards** are offered | The stack has no monitoring. | Edit the stack, turn on **Deploy monitoring (Prometheus)** and save. |
| My application's metrics are missing | Prometheus only scrapes what a `ServiceMonitor` or `PodMonitor` points it at. | Add one for your application. If the target shows `TargetDown`, check that the observability nodes can reach its port. |
| Volumes stay Pending | No StorageClass could be used for them. | Mark a StorageClass as default. |

## If something was left behind

- **Kept by design**: the log bucket, Prometheus volume, S3 VPC endpoint, security group rules the stack added, the namespace and the OIDC provider. Delete them yourself if you no longer need them. The teardown preview prints the command to delete the Prometheus volume.
- **A teardown that ended Failed**: its status names what's left. Select **Deprovision** again to pick up where it stopped.
- **A stack record deleted without teardown**: its resources are still in AWS and the cluster. The node group is named `<cluster>-observability-nodepool`, and the bucket is named `<stack name>-logs-<random>`.

## FAQ

**Does it install the load balancer controller, autoscaler or external-dns?**
No. They're shared cluster add-ons you provide. The wizard checks for them.

**What is the difference between the two modes?**
**Standalone** needs only an AWS scope and a Kubernetes scope. **Use the DevOps extension** also ties the stack to a DevOps environment and resource group, and is offered only where that extension is available. You can't change the mode later.

**Where do my logs go, and for how long?**
To the stack's S3 bucket through Loki. They're kept for one year by default, and you can change that on **Log Storage**.

**Does Prometheus send alerts?**
No. There's no Alertmanager. Alerts are visible in Prometheus and in Grafana.

**Can other clusters send logs and metrics in?**
Yes. Turn on the internal Loki or Prometheus endpoint, and point collectors in the other clusters at the addresses on the **Loki** and **Monitoring** tabs. They must be in the same VPC or a peered network.

**Does tearing down delete my logs?**
No. The log bucket and the Prometheus volume are kept.

**Can I make Grafana private?**
Not from the wizard. Grafana always gets a public load balancer, with sign-in through your portal.
