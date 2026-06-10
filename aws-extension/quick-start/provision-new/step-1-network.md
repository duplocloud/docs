---
description: Create a Network Baseline — a VPC with public and private subnets across multiple availability zones.
---

# Step 1: Create a Network

A Network Baseline provisions the VPC that all other resources will run inside. This is the first resource you create.

## What gets created

* A VPC with your chosen CIDR block
* Public and private subnets, one pair per availability zone
* An Internet Gateway for public subnet routing
* NAT Gateways for private subnet outbound access (if enabled)
* Route tables for public and private subnets
* RDS and ElastiCache subnet groups pre-configured for databases

## Walkthrough

### Step 1 — Navigate to Network

In the left sidebar, click **DevOps** and select **Network** from the submenu.

![](<../../../.gitbook/assets/network-step-01.png>)

### Step 2 — Network List

The Network page lists all provisioned networks. When starting fresh the list is empty. Click **+ Create network** to begin.

![](<../../../.gitbook/assets/network-step-02.png>)

### Step 3 — Network Details

The **Create Network Baseline** wizard opens. Fill in the first page:

* **Name** — a unique identifier for the network (e.g. `prod-network-1`)
* **Description** — optional
* **Account (Scope)** — the cloud account scope to provision into (e.g. `full-access-us-east-1`)
* **Skills** — optional; attach custom skills to this network

Click **Next**.

![](<../../../.gitbook/assets/network-step-03.png>)

### Step 4 — Network Spec

Define the network configuration. Select **Create new** to provision a fresh VPC, or **Import existing** to register an existing one.

* **Region** — the AWS region (e.g. `us-east-1 — N. Virginia`)
* **VPC CIDR** — the IP range for the VPC (e.g. `10.0.0.8/16`). The platform checks for overlap with existing networks.
* **Availability Zones** — number of AZs to span (e.g. `2`)
* **NAT Gateway** — choose `None`, `Single NAT Gateway`, or one per AZ
* **Subnet Prefix** — host bits per subnet (e.g. `24`)

The **Subnets — computed from CIDR** table previews the private and public subnet CIDRs that will be created per AZ before you submit.

Click **Create & Provision**.

![](<../../../.gitbook/assets/network-step-04.png>)

### Step 5 — Agent Ticket Opens

Clicking Create & Provision automatically opens an agent ticket. The agent uses the `duplo-aws-infra` skill and begins by reading the `aws-network-baseline.md` skill file to load its instructions.

![](<../../../.gitbook/assets/network-step-05.png>)

### Step 6 — Parameters Parsed

The agent sets up AWS credentials, then parses the network spec into structured parameters:

* `NETWORK_NAME`, `REGION`, `VPC_CIDR`, `azs`, `subnet_mask`
* `NAT_MODE` (e.g. `SingleAz`), `ENABLE_DNS`, `ENABLE_FLOW_LOGS`
* `FLOW_LOGS_RETENTION_DAYS`, `ENV_TAG`

These values drive every subsequent step of the provisioning workflow.

![](<../../../.gitbook/assets/network-step-06.png>)

### Step 7 — Phase 1: Validate

The agent runs **Phase 1 — Parse & Validate**:

* **Step 1.2** — Validates the region exists and is accessible
* **Step 1.3** — Resolves availability zone names (e.g. `us-east-1a`, `us-east-1b`) for the selected region
* **Step 1.4** — Validates the subnet mask and computes the full CIDR layout

![](<../../../.gitbook/assets/network-step-07.png>)

### Step 8 — Phase 2: Compute

**Phase 2 — Compute** calculates the exact subnet CIDRs and resource counts:

* **Step 2.1** — Computes public and private subnet CIDRs per AZ from the VPC CIDR block
* **Step 2.2** — Determines NAT configuration (EIP count, NAT count, private route table count)
* **Step 2.3** — Tallies the total number of AWS resources to be created (e.g. 14)

Then **Phase 3 — Provision via CloudFormation** begins with Step 4.0 deriving the CloudFormation stack name.

![](<../../../.gitbook/assets/network-step-08.png>)

### Step 9 — Pre-flight Checks

Before creating the stack the agent runs two pre-flight checks:

* **Step 4.1** — Checks whether the stack already exists to avoid duplicate provisioning
* **Step 4.1b** — VPC CIDR preflight: confirms no existing VPC uses the same CIDR block in the account

If both checks pass, the agent proceeds to stack creation.

![](<../../../.gitbook/assets/network-step-09.png>)

### Step 10 — CloudFormation Stack Created

* **Step 4.2** — Deploys the CloudFormation template, creating the stack
* **Step 4.3** — Starts an event-stream polling loop that tracks stack events in real time for up to 15 minutes, reporting each resource as it is created

![](<../../../.gitbook/assets/network-step-10.png>)

### Step 11 — Stack Outputs Retrieved

**Phase 5 — Finalize** begins once the stack completes:

* **Step 5.1** — Reads all stack outputs (VPC ID, subnet IDs, route table IDs, NAT gateway ID, etc.)

![](<../../../.gitbook/assets/network-step-11.png>)

### Step 12 — Runtime Details Enriched

* **Step 5.2** — Queries AWS at runtime to enrich the output with additional subnet metadata (CIDR blocks, AZ assignments, tags) that CloudFormation outputs alone don't include

![](<../../../.gitbook/assets/network-step-12.png>)

### Step 13 — Output Written

* **Step 5.3** — Builds the structured `output.json` file from the enriched data, validated against the skill's output schema, and writes it to the ticket for downstream provisioning steps (Plan, Cluster, Environment)

![](<../../../.gitbook/assets/network-step-13.png>)

### Step 14 — Provisioning Complete

The agent reports **Step 5.5 — Completion**. The network baseline is fully provisioned. The summary confirms:

* VPC created with the specified CIDR in the selected region
* 2 public and 2 private subnets across the selected AZs
* 1 NAT gateway with an associated Elastic IP
* Internet gateway, route tables, and subnet–route table associations

![](<../../../.gitbook/assets/network-step-14.png>)

## Next step

Once the Network Baseline status shows **Ready**, proceed to [Step 2: Create a Cluster](step-2-cluster.md).
