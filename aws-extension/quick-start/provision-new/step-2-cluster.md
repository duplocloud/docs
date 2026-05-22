---
description: Create a Cluster Baseline — an EKS cluster built on top of your Network Baseline.
---

# Step 2: Create a Cluster

A Cluster Baseline provisions an EKS cluster inside the Network you created in the previous step. The VPC, region, and subnets are inherited automatically from the Network Baseline.

## What gets created

* An EKS cluster with your chosen Kubernetes version
* Cluster IAM role and service account configuration
* OIDC provider for IAM Roles for Service Accounts (IRSA)
* A Kubernetes Provider and Scope automatically connected to the new cluster

## Walkthrough

### Step 1 — Navigate to Cluster

In the left sidebar, click **DevOps** and select **Cluster** from the submenu.

![](<../../../.gitbook/assets/cluster-step-01.png>)

### Step 2 — Cluster List

The Cluster page lists all existing clusters with their type, EKS version, status, and mode. When starting fresh the list is empty. Click **+ Create cluster** to begin.

![](<../../../.gitbook/assets/cluster-step-02.png>)

### Step 3 — Cluster Details

The **Create Cluster Baseline** wizard opens. Fill in the first page:

* **Name** — a unique identifier for the cluster (e.g. `prod-eks-cluster`)
* **Description** — optional
* **Account (Scope)** — the cloud account scope to provision into (e.g. `full-access-us-east-1`)
* **Skills** — optional; attach custom skills to this cluster

Click **Next**.

![](<../../../.gitbook/assets/cluster-step-03.png>)

### Step 4 — Cluster Spec

Define the cluster configuration. Select **Create new** to provision a fresh EKS cluster, or **Import existing** to register an existing one.

* **Network Source** — select **Choose Network** to inherit VPC and subnet details from a provisioned network baseline
* **Network** — select the network (e.g. `prod-network-1`). Region, VPC ID, and subnet IDs are inherited automatically.
* **Cluster Type** — `Standard`
* **EKS Version** — the Kubernetes version to deploy (e.g. `1.33`). This field is required even if the UI labels it optional.
* **API Server Visibility** — `Public` exposes the Kubernetes API endpoint publicly; `Private` restricts it to the VPC
* **Control Plane Logging** — optional; select which EKS control plane log types to enable (API, Audit, Authenticator, etc.)
* **Cluster IP CIDR** — optional; leave blank to use the EKS default (`172.20.0.0/16`)

Click **Create & Provision**.

![](<../../../.gitbook/assets/cluster-step-04.png>)

### Step 5 — Provisioning Started

The cluster detail page opens immediately with **Status: Pending**. The spec summary confirms:

* Cluster type: Standard
* EKS version: 1.33
* API server visibility: Public
* Cluster IP CIDR: Default
* Control plane logging: None

Click **Track Provisioning Status** to open the agent ticket and follow the provisioning workflow in real time.

![](<../../../.gitbook/assets/cluster-step-05.png>)

### Step 6 — Agent Ticket Opens

The agent opens a ticket and begins the provisioning workflow using the `duplo-aws-infra` skill. The initial phases run immediately:

* **Phase 0 — Acknowledge**: The agent reads the `aws-cluster-baseline.json` skill file to load its provisioning instructions.
* **Phase 0.5 — AWS\_PROFILE guard**: Confirms that AWS credentials are correctly configured for the target account before proceeding.
* **Phase 1 — Parse & Validate**: Begins parsing the cluster specification passed from the UI.

![](<../../../.gitbook/assets/cluster-step-06.png>)

### Step 7 — Phase 1: Parse & Validate

The agent extracts and validates all fields from the cluster object:

* `name`, `vpcId`, `region`, `subnets` — inherited from the linked Network Baseline
* `clusterType` — `Standard`
* `eksVersion` — `1.33`
* `apiServerVisibility` — normalized to lowercase (`public`)

The agent then validates that the resolved region is accessible before advancing to computation.

![](<../../../.gitbook/assets/cluster-step-07.png>)

### Step 8 — Phase 2: Compute & Phase 3: Provision

**Phase 2 — Compute** derives the resources needed:

* EKS IAM role name (derived from the cluster name)
* AMI type for managed node groups

**Phase 3 — Provision via CloudFormation** then begins:

* Derives the CloudFormation stack name from the cluster name
* Checks whether the stack already exists to prevent duplicate provisioning
* Deploys the CloudFormation template, creating the EKS cluster, IAM roles, and associated resources
* Polls stack events in real time, reporting each resource as it is created

![](<../../../.gitbook/assets/cluster-step-08.png>)

### Step 9 — Stack Outputs & OIDC Provider

Once the CloudFormation stack completes, the agent runs finalization steps:

* **Step 4.2.3** — Reads all stack outputs: cluster ARN, API endpoint, certificate authority (CA) data, security group IDs, and subnet associations. Posts the full CA data and parses the result back to the controller.
* **Step 4.2 — Create OIDC identity provider**: Registers the cluster's OIDC issuer URL as a trusted identity provider in IAM, enabling IAM Roles for Service Accounts (IRSA).

![](<../../../.gitbook/assets/cluster-step-09.png>)

### Step 10 — Output Validation & Completion

The agent finalizes the provisioning:

* **Step 4.3** — Validates the assembled `output.json` against the skill's output schema to confirm all required fields are present and correctly typed.
* **Step 5** — Posts the final results to the controller and sets the cluster status to **Complete**.
* **Step 5.5** — Reports the provisioning completion summary with all key cluster details.

![](<../../../.gitbook/assets/cluster-step-10.png>)

### Step 11 — Provisioning Complete

The agent reports **Step 5.5 — Completion**. The EKS cluster is fully provisioned. The summary confirms:

* **EKS Cluster ARN** — the full Amazon Resource Name for the cluster
* **API Endpoint** — the Kubernetes API server URL
* **OIDC Issuer URL** — the identity provider URL for IRSA configuration
* **Cluster Security Group** — the security group attached to the EKS control plane
* **All-Host Security Group** — the security group applied to all worker nodes
* **CloudFormation Stack** — the stack name managing all provisioned resources

![](<../../../.gitbook/assets/cluster-step-11.png>)

### Step 12 — Cluster List: Ready

After provisioning completes the Cluster list shows `prod-eks-cluster` with **Status: Ready**, type **Standard**, and EKS version **1.33**. The three-dot menu on any cluster row gives access to **View**, **Deprovision**, and **Delete**.

![](<../../../.gitbook/assets/cluster-step-12.png>)

### Step 13 — Cluster Overview

Click into the cluster to open the detail page. The **Overview** tab displays all key cluster identifiers:

* **Cluster ARN** — `arn:aws:eks:us-east-1:813590939111:cluster/prod-eks-cluster`
* **API Endpoint** — the Kubernetes API server URL (`*.gr7.us-east-1.eks.amazonaws.com`)
* **OIDC Issuer URL** — used to configure IAM Roles for Service Accounts (IRSA)
* **Certificate Authority** — the base64-encoded CA data for `kubectl` configuration

The left sidebar exposes full cluster navigation: **Workloads** (Pods, Deployments, StatefulSets, DaemonSets, Jobs, CronJobs), **Configs**, **Network**, **Volumes**, and **Observe**.

![](<../../../.gitbook/assets/cluster-step-13.png>)

### Step 14 — Cluster Attributes

Click **Attributes** in the sidebar to configure optional Kubernetes components and EKS add-ons. The **Configure Cluster Attributes** panel lists all available components:

* Cluster Autoscaler
* Secret CSI Driver
* ALB Load Balancer Controller
* EFS Volumes
* Metrics Server
* Kube State Metrics
* Flux CD
* External DNS

Each component can be individually enabled. The **EKS Addons** section allows installing managed AWS add-ons via **+ Add Addon**. Click **Configure** to apply selections.

![](<../../../.gitbook/assets/cluster-step-14.png>)

### Step 15 — Selecting Components

Check the components you want enabled on the cluster. Each checkbox enables that controller or add-on during the next attributes provisioning run. Components can be enabled incrementally — you do not need to select all at once.

![](<../../../.gitbook/assets/cluster-step-15.png>)

### Step 16 — External DNS Domain Filters

When **External DNS** is enabled, a **Domain Filters** field appears requiring at least one domain. Enter the Route 53 hosted zone domain (e.g. `example.com`) and click **+ Add Domain** for additional domains. External DNS will only manage records within the specified domains.

![](<../../../.gitbook/assets/cluster-step-16.png>)

### Step 17 — Attributes Saved

After clicking **Configure**, the attributes are saved as a named configuration object (`prod-eks-cluster-attributes`) with **Status: New** while the agent applies the changes. The summary lists each component and its enabled/disabled state:

| Component | Status |
|---|---|
| Cluster Autoscaler | Enabled |
| Secret CSI Driver | Enabled |
| ALB Load Balancer Controller | Enabled |
| EFS Volumes | Enabled |
| Metrics Server | Enabled |
| Kube State Metrics | Enabled |
| Flux CD | Enabled |
| External DNS | Disabled |

Click **Track Provisioning Status** to follow the agent as it installs the selected components into the cluster.

![](<../../../.gitbook/assets/cluster-step-17.png>)

## Next step

Once the Cluster Baseline status shows **Ready**, proceed to [Step 3: Create an Environment](step-3-environment.md).
