---
description: What Standard Observability can read and change, which actions need approval, and how it behaves for read-only, regular and admin users.
---

# Permissions and Safety

## What it can read and change

Standard Observability acts with the IAM identity of the AWS scope and the Kubernetes identity of the Kubernetes scope you choose. In DevOps extension mode some changes are made through the DuploCloud platform (node pool, S3 bucket, ingresses) instead of the AWS command line.

| | What it does |
| --- | --- |
| **Reads** | Your EKS cluster and its VPC, route tables, subnets and security group rules, the EC2 instances in the cluster, ACM certificates and EKS clusters (for the wizard lists), the cluster's add-ons, StorageClasses, existing Prometheus Operators, and the state of its own Helm releases. |
| **Changes in AWS** | Creates an EKS node group (`<cluster>-observability-nodepool`). Adds security group rules (one source group and one port each, described `standard-observability ...`). Creates an S3 gateway VPC endpoint, or adds route tables to an existing one. Creates an S3 log bucket. Creates load balancers through Kubernetes Ingresses: a public (internet-facing) one for Grafana and optional internal ones for Loki and Prometheus. |
| **Changes in IAM (standalone mode)** | Creates a node IAM role (`<cluster>-observability-node`, with the three standard EKS node policies) unless you supply one. Creates the cluster's IAM OIDC provider if it is missing. Creates or updates a role `<cluster>-observability-s3` that trusts only the `observability-s3` service account and is limited to the log bucket. If that role already exists, its trust policy and its inline policy `observability-logs-s3` are rewritten on every run. |
| **Changes in DNS** | None directly. With **Create it automatically (external-dns)** the ingress carries an external-dns hostname annotation and external-dns on your cluster creates the Route 53 record. Otherwise you create the record yourself. |
| **Changes in Kubernetes** | Creates the namespace (default `observability`) if missing. Applies Flux Helm repositories and releases for Loki, Grafana, the log collectors and (if enabled) Prometheus. Creates Secrets (`grafana-admin`, `grafana-proxy`), a NetworkPolicy so only the sign-in proxy reaches Grafana, the sign-in proxy deployment and service, Ingresses and, in standalone mode, the `observability-s3` service account. In DevOps extension mode it also turns on the FluxCD flag in the cluster's settings. It never turns add-ons off. |
| **Never** | It does not edit or remove existing security group rules. It does not delete your log bucket, S3 VPC endpoint, namespace, metric volume, shared add-ons or the OIDC provider. It does not touch an existing object it did not create (an existing role, node group, bucket or namespace you supplied is used as is and is never deleted). It does not install the load balancer controller, autoscaler or external-dns. |

{% hint style="warning" %}
The Grafana load balancer is internet-facing. Access is controlled by sign-in through your DuploCloud portal, and a NetworkPolicy keeps other pods away from Grafana. Choose your certificate and DNS name with that in mind.
{% endhint %}

<!-- VERIFY: "internet-facing" comes from the ingress annotation scheme for non-internal endpoints. Confirm there is no way to make Grafana internal-only. -->
<!-- VERIFY: QA on 2026-11-18 saw Route 53 record-set permissions and iam:UpdateAssumeRolePolicy needed. The IAM update is confirmed in standalone code (role rewrite above). Route 53 is not called by the extension code; confirm whether the platform or external-dns makes those calls. -->

## Who can do what

The extension does not define its own permission names. Its screens and actions rely on the DuploCloud platform permissions for workspace resources, plus two places where it needs the Administrator role.

| Action | Who | Notes |
| --- | --- | --- |
| View stacks, the stack page and dashboards | Anyone with access to the workspace resource | The platform decides this. |
| Create, edit, deprovision or delete a stack | Users the platform permits to write this resource type | Starts or re-runs provisioning, which changes AWS and Kubernetes. |
| Recheck the DNS endpoint | Anyone who can see the stack | Read-only probe, then updates the stack status. |
| Associate an existing Grafana scope | Anyone who can see the stack | Records a scope id on the stack only. |
| Create the Grafana scope | **Administrator** | Creating the provider and scope is an administrator-only platform write. Others get a 403 and are sent to "Associate an existing scope". |
| Allow-list the Grafana host for sign-in | **Administrator** | Done once in System Config. |
| Curate favourites | Anyone who can edit the stack | Does not re-run provisioning. |

| User | What they can do |
| --- | --- |
| **Read-only** | UNKNOWN. The extension has no read-only handling of its own: its create, edit, deprovision, delete and favourites controls are not disabled by role in the code. Whether the platform blocks a read-only user depends on the platform's permission model for this resource type. |
| **Regular user** | What the platform's permission sets grant for this resource type in the workspace. Cannot create a Grafana scope; can associate an existing one. |
| **Administrator** | Everything, including creating the Grafana scope and the sign-in allow-list entry. |

<!-- VERIFY: the whole role table. The repo has no [AccessControl] attributes, no permission verbs, no UI disabled states by role and no administrator override. The only role logic is the 401/403 handling for the admin-only Grafana scope calls (the Create button disappears after the first refusal). Pankaj Akhade and Srikar Naramsetty decide admin-only versus user on ClickUp 17twvjx4bm3. Rewrite after that decision and test with read-only, regular and admin users in QA (screenshots SO-18 to SO-21). -->
<!-- VERIFY: the Grafana local admin password is stored on the stack record and shown on the stack page with Reveal and Copy to anyone who can open the page. Confirm whether that should be limited to administrators. The extension README claims no shared admin password is in circulation, which this contradicts. -->

## What needs approval

- **Submitting the wizard.** Nothing is created until you submit on the Review step. There is no separate plan approval step.
- **Deprovision.** The portal asks you to confirm twice and shows what is removed and what is kept. The provisioning agent is also instructed to print a dry run and wait for your written confirmation in the ticket chat; a repeated generic "Deprovision this resource" message does not count as confirmation.
- **Editing a stack.** Saving re-runs provisioning with no extra prompt.
- **The agent.** The agent that runs the work is instructed to run only the bundled script, and, if it fails, to report and stop: no manual `kubectl delete`, `helm uninstall`, AWS writes, or hand-made fixes to DNS, IAM, node groups or security groups.

<!-- VERIFY: the teardown confirmation and the "report and stop" rule are instructions to the AI agent in the skill, not enforced by code. In the script, the real teardown runs when started without the dry-run flag. Confirm whether the platform adds a hard approval gate. -->

## Safety checks

- **Fail before creating.** The S3 VPC endpoint is checked with an EC2 dry run first. If it cannot be created, the stack fails with nothing created. There is no fallback to the NAT gateway.
- **Narrow security group rules.** The stack only adds single-source, single-port ingress rules it needs, and fails listing them if the role cannot add them.
- **Foreign objects are protected.** Before applying any object, the stack checks whether one with the same name already exists and is not its own; if so it stops and names it.
- **Created-by-this-stack ledger (standalone).** Teardown deletes only objects recorded as created by the stack, in reverse order, and resumes if interrupted.
- **Existing namespace is respected.** An existing namespace is used as is, not relabelled and never deleted.
- **Logs and metrics are kept.** Teardown keeps the log bucket and the Prometheus volume, and prints the command to delete the volume yourself.
- **Prometheus conflict check.** An active cluster-wide Prometheus Operator elsewhere fails the run before anything is installed; a paused one is a warning.
- **Admin password is not placed in chart values.** It is written to the `grafana-admin` Secret.
- **One run at a time per stack.** A second run reports "another run already in progress" and stops.

## Limits you should know

- Standard Observability does not roll back: a failed run leaves what it created. Fix the cause and run it again.
- The node pool, load balancers, EBS volumes and S3 storage are billed by AWS.
- Teardown keeps the log bucket, S3 VPC endpoint, namespace, Prometheus volume and shared add-ons. Remove them yourself if you no longer need them.
- Prometheus has no Alertmanager: alerts are visible in Prometheus and Grafana but are not sent anywhere.
- Mode, cluster, environment, resource group and namespace cannot be changed after creation.

## AI data handling

<!-- VERIFY: the repo does not describe what is sent to the AI model beyond the ticket the provisioning agent works in. The agent reads the stack's settings and scope credentials in its working directory and is told not to open or print them. Ask the owners what data goes to the model and how long tickets are kept before writing this section. -->
