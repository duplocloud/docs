---
description: Common problems with Standard Observability and how to fix them.
---

# Troubleshooting and FAQ

## Common problems

| What you see | What it means | What to do |
| --- | --- | --- |
| **Stack is Blocked with "create this DNS record"** | You chose "I will create it". Grafana is unreachable until the record exists. | Create the record shown, then select **I've created it - re-check**. |
| **Record exists but re-check says the endpoint is not responding** | DNS is correct but the load balancer's target group may still be unhealthy. | Wait a minute and re-check. |
| **Browser stops at "Redirecting to .../duplo_auth/bridge"** | The Grafana host is not on the sign-in allow-list. | Ask a DuploCloud Administrator to add `AppConfig/otel` = `https://<grafana hostname>` in System Config. |
| **"Action required - register the Grafana scope"** | Grafana is reachable but no scope is registered. | An administrator selects **Create Grafana scope**, or you associate an existing scope. |
| **Create Grafana scope is refused or missing** | Only administrators can create the provider and scope. | Associate a scope an administrator already attached to the workspace. |
| **Fails early at AWS preflight (S3 VPC endpoint)** | The AWS scope's role cannot read or create the VPC endpoint, or the VPC or route tables could not be found. Nothing was created. | Grant the EC2 permissions on [Set Up](set-up.md), then edit and save the stack to run it again. |
| **Fails at Node networking, listing rules** | The role cannot add security group rules. | Add the listed rules yourself or grant `ec2:AuthorizeSecurityGroupIngress`, then run again. Do not widen the rules beyond the ones listed. |
| **Fails: an active Prometheus Operator is already in the cluster** | Two cluster-wide operators would fight over the same objects. | Remove or pause the other operator, or turn Monitoring off. |
| **Fails: no usable StorageClass for Prometheus** | The cluster has no StorageClass for the volume. | Create a StorageClass and mark it default. |
| **Volumes stay Pending** | The cluster has no default StorageClass (a warning, not a failure). | Mark a StorageClass as default. |
| **Run stops naming an existing object** | An object with the same name exists in the namespace and was not created by this stack. | Rename or remove your object, or choose another namespace. The stack never overwrites it. |
| **Standalone run fails on FluxCD** | FluxCD is required and is not installed by the stack. | Install FluxCD on the cluster, then run again. |
| **Warning: missing autoscaler, load balancer controller or external-dns** | These are cluster prerequisites. The run records `missing` and continues. | Install the add-on. Without the load balancer controller the Grafana endpoint will not come up. |
| **Admin password rejected** | It must be at least 8 characters with upper-case, lower-case, a digit and a special character. | Choose a stronger password. |
| **"Another run already in progress"** | Another provisioning session holds the ticket. | Wait for it to finish. Nothing was changed by the second request. |
| **Dashboards page shows only Explore** | The stack was created without Monitoring. | Edit the stack, turn Monitoring on and save. |

<!-- VERIFY: error messages are paraphrased from the code and skill, not seen in QA. Confirm wording. A failed run is retried by saving the stack from Edit: confirm. -->

## If something was left behind

- Security group rules the stack added are never removed. Look for rules described `standard-observability ...`.
- The Prometheus volume is kept after teardown. The teardown preview prints the `kubectl delete pvc` command.
- If a teardown ends as Failed, its message names what survived; running Deprovision again resumes where it stopped (standalone).

<!-- VERIFY: manual cleanup commands for orphaned IAM roles and the node group are not in the repo. Ask the owners for a recovery list. -->

## FAQ

**Does it install the load balancer controller, autoscaler or external-dns?** No. They are shared cluster add-ons you provide. It only enables the FluxCD flag in DevOps extension mode.

**What is the difference between the two modes?** DevOps extension mode uses the workspace's Environment, Resource Group and portal records. Standalone mode needs only an AWS scope and a Kubernetes scope and applies everything with the AWS CLI and `kubectl`. The mode is fixed once the stack exists.

**Where do my logs go?** To an S3 bucket through Loki. They are kept for 8760 hours (one year) by default.

**Does Prometheus send alerts?** No. There is no Alertmanager.

**Can I send logs from other clusters?** Yes, by enabling the internal Loki endpoint and pointing collectors at the push URL on the result page.

**Does Deprovision delete my logs?** No. The bucket, the Prometheus volume and the S3 VPC endpoint are kept.

**What does it cost?** UNKNOWN. See the Overview.

<!-- VERIFY: FAQ is a first guess from the code. Owners to add real customer questions. -->
