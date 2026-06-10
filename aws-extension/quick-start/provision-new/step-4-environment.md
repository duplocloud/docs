---
description: Create an Environment — a deployment boundary inside your cluster with dedicated IAM and network isolation.
---

# Step 4: Create an Environment

An Environment is a deployment boundary inside the Cluster you created in Step 2. It provisions dedicated security groups, IAM roles, and KMS keys scoped to this environment. Attaching the Plan you created in Step 3 makes its hosted zones and certificates available to workloads and load balancers in this Environment.

## What gets created

* Security groups controlling inbound and outbound traffic for resources in this Environment
* IAM roles scoped to the Environment for workloads and service accounts
* KMS encryption keys for secrets and storage

## Walkthrough

### Step 1 — Navigate to Environments

In the left sidebar, click **DevOps** and select **Environments** from the submenu. The Environments page lists all existing environments with their name, description, resource group count, created date, and last modified date. When starting fresh the list is empty. Click **+ Create environment** to begin.

![](<../../../.gitbook/assets/environment-step-01.png>)

### Step 2 — Create Environment

The **Create environment** modal opens. Fill in:

* **Name** — a unique identifier for the environment (e.g. `prod-environment`)
* **Description** — optional
* **Plans** — optional; associate one or more Plans to contribute reusable AWS references (AMIs, certificates, hosted zones) to this environment

![](<../../../.gitbook/assets/environment-step-02.png>)

### Step 3 — Associate a Plan

Open the **Plans** dropdown to see all available plans in the workspace. Select the plan created in the previous step (e.g. `prod-plan`). The selected plan appears as a chip in the field. Plans make their AMI, certificate, and hosted zone references available to all Resource Groups within this environment.

Click **Create**.

![](<../../../.gitbook/assets/environment-step-03.png>)

### Step 4 — Environment Created

The environment detail page opens immediately. The **Resource Group** selector shows **None** and the page displays an empty state:

> A Resource Group is a container of resources. When the resources are created via DuploCloud all resources in the resource group share the security profile and hence ResourceGroup is a security boundary. When external resources are imported in a group then it is more of a logical grouping of resources.

Click **+ Create Resource Group** to add the first resource group.

![](<../../../.gitbook/assets/environment-step-04.png>)

### Step 5 — Resource Group Details

The **Create Resource Group** wizard opens. Fill in the Details page:

* **Name** — a unique identifier for the resource group (e.g. `prod-resourcegroup-1`)
* **Description** — optional
* **Skills** — optional; attach custom skills to this resource group

Click **Next**.

![](<../../../.gitbook/assets/environment-step-05.png>)

### Step 6 — Resource Group Spec

The Spec page links the resource group to its underlying infrastructure. The agent will use these selections to provision IAM policies, an IAM role, a KMS key, and security groups.

* **Network Baseline** — select the network provisioned earlier (e.g. `prod-network-1`). The VPC and region are inherited automatically from this selection.
* **Kubernetes Cluster** — select the EKS cluster provisioned earlier (e.g. `prod-eks-cluster`). Only clusters with **Status: Ready** are listed. Namespaces and workloads created under this resource group will be provisioned into the selected cluster.

Click **Create & Provision**.

![](<../../../.gitbook/assets/environment-step-06.png>)

### Step 7 — Provisioning Started

The resource group detail page opens with **Status: Provisioning**. The Spec tab confirms the inherited configuration:

* **Region**: `us-east-1` (inherited from the Network Baseline)
* **VPC ID**: the VPC provisioned with the network
* **Cluster**: `prod-eks-cluster`

The left sidebar exposes the full resource group navigation: **Micro Services**, **Kubernetes** (Namespaces, Nodes, Workloads, Configs, Storage, Networks), **Cloud Resources** (Hosts, Serverless, Storage, Databases, Networks, Configs), and **Observability**.

Click **Track Provisioning Status** to follow the agent workflow in real time.

![](<../../../.gitbook/assets/environment-step-07.png>)

### Step 8 — Agent Ticket Opens

The agent opens a ticket titled **ResourceGroup Resource Management — prod-resourcegroup-1** using the `duplo-aws-infra` skill. It reads the task file to locate the handler for ResourceGroup provisioning, sets up AWS credentials, and begins checking for a pre-existing CloudFormation stack.

![](<../../../.gitbook/assets/environment-step-08.png>)

### Step 9 — Parameters Resolved & Stack Check

The agent resolves all required variables:

* Sets `REGION` and exports `AWS_SHARED_CREDENTIALS_FILE`
* Resolves `RESOURCE_GROUP_ID` and `WORKSPACE_ID` from the resource group object
* Confirms both region (`us-east-1`) and VPC ID are set
* Derives the CloudFormation stack name from the resource group details
* Checks whether a stack already exists to prevent duplicate provisioning

![](<../../../.gitbook/assets/environment-step-09.png>)

### Step 10 — Stack Submitted

Finding no pre-existing stack, the agent submits the CloudFormation template and begins polling for partial results as each resource completes. Stack events are reported in real time as the security groups, IAM role, and KMS key are created.

![](<../../../.gitbook/assets/environment-step-10.png>)

### Step 11 — Provisioning Complete

The agent writes the `output.json` file, posts the final results, and marks the resource group **Complete**. The completion summary lists all provisioned resources:

| Resource | ID |
|---|---|
| **Security Group** | `duplo-rb-prod-environment-prod-resourcegroup-1` |
| **ALB Security Group** | `duplo-rb-prod-environment-prod-resourcegroup-1-alb` |
| **IAM Role** | `arn:aws:iam::…/duplo-rb-prod-environment-prod-resourcegroup-1` |
| **KMS Key** | `arn:aws:kms:us-east-1:…` |

All resources are live in `us-east-1`. The resource group status is set to **Complete** and the environment is ready for workload deployment.

![](<../../../.gitbook/assets/environment-step-11.png>)

## Next step

Once the Environment status shows **Ready**, proceed to [Step 5: Deploy Workloads](step-5-workloads.md).
