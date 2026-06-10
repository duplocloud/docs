---
description: Create a Plan — an account-level catalog of hosted zones, ACM certificates, and AMIs.
---

# Step 3: Create a Plan

A Plan catalogs the AWS account-level resources your environments and workloads will reference — Route 53 hosted zones for DNS, ACM certificates for TLS, and AMIs for compute. Creating a Plan before the Environment means you can attach it at Environment creation time.

## What gets created

* A catalog of Route 53 hosted zones available in your account and region
* A list of ACM certificates with their domain names and ARNs
* A list of AMIs available for workload and host provisioning

## Walkthrough

### Step 1 — Navigate to Plans

In the left sidebar, click **DevOps** and select **Plans** from the submenu.

![](<../../../.gitbook/assets/plan-step-03.png>)

### Step 2 — Plans List

The Plans page lists all existing plans with their region, hosted zone, certificate count, AMI count, and description. When starting fresh the list is empty. Click **+ Create plan** to begin.

![](<../../../.gitbook/assets/plan-step-04.png>)

### Step 3 — Plan Details

The **Create Plan** wizard opens. Fill in:

* **Name** — a unique identifier (e.g. `prod-plan`)
* **Description** — optional
* **Region source** — select **Inherit from a Network Baseline** to derive the region automatically from the linked network
* **Network Baseline** — select the network provisioned in the previous step (e.g. `prod-network-1`). The resolved region is shown below the field.

Click **Next**.

![](<../../../.gitbook/assets/plan-step-05.png>)

### Step 4 — References

The References page collects optional DNS and certificate configuration:

* **Primary hosted zone** — Hosted zone ID and domain name from Route 53
* **Certificates** — ACM certificate ARNs and their associated domains
* **AMIs** — custom AMI IDs for node provisioning

All fields are optional. The hint at the top of the page notes that you can leave everything blank and use the **Configure using agent** button after creation to let the agent look up and populate these values from your AWS account automatically.

Click **Create Plan**.

![](<../../../.gitbook/assets/plan-step-06.png>)

### Step 5 — Plan Created

A success banner confirms the plan was created. The plan detail page opens with **Status: Ready**, showing the region and linked Network Baseline. Three tabs — **Primary hosted zone**, **Certificates**, and **AMIs** — are available for managing references. The sidebar shows counts for each.

Click **Configure using agent** to populate references from your AWS account.

![](<../../../.gitbook/assets/plan-step-07.png>)

### Step 6 — Start Agent Session

The **Configure using agent** modal opens. Select the cloud **Scope** that gives the agent access to your AWS account (e.g. `full-access-us-east-1`). The selected scope is saved to the plan and reused for all future agent sessions.

Click **Start agent session**.

![](<../../../.gitbook/assets/plan-step-08.png>)

### Step 7 — Agent Lists Available Resources

The agent opens a ticket, queries your AWS account for the plan's region, and lists all available resources:

* **Hosted Zones** — Route 53 hosted zones with their IDs
* **Certificates** — ACM certificates (issued only), with ARN, domain, validity dates, and renewal status. Expired certificates are listed separately and available on request.

The agent shows the current plan state and provides shortcuts for making selections:

* `hz:1` — set hosted zone 1 as primary
* `certs:1` — add certificate 1
* `hz:1 certs:1` — do both at once
* `skip.hz` / `skip.certs` — skip a group
* `amis` — browse AMIs next

![](<../../../.gitbook/assets/plan-step-10.png>)

### Step 8 — Plan Updated

After you reply with your selections (e.g. `add certificate 1 and set hosted zone 1 as primary`), the agent re-reads the current plan, applies the changes, and confirms:

* **Primary hosted zone** set to the selected domain
* **Certificates** updated with the selected ACM certificate

The agent then asks if you want to add AMIs next or are all set.

![](<../../../.gitbook/assets/plan-step-09.png>)

## Next step

Once the Plan is ready, proceed to [Step 4: Create an Environment](step-4-environment.md).
