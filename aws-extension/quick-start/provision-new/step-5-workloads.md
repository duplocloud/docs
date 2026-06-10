---
description: Deploy a workload into your Environment — create a Namespace and a Deployment.
---

# Step 5: Deploy Workloads

With your Environment ready, you can now deploy applications. This step creates a Namespace and a Deployment inside it.

## What you will do

* Create a Namespace inside the Environment
* Create a Node Group to provide compute capacity for the cluster
* Create a Deployment with your container image
* Optionally attach a load balancer to expose the application externally, using the hosted zone and certificate from your Plan

## Walkthrough

### Step 1 — Resource Group Ready

Once the Resource Group finishes provisioning its **Status** changes to **Ready**. The Overview tab shows the provisioned AWS resources — security groups, IAM role, and KMS key — that define the security boundary for this resource group. The left sidebar now shows the full resource group navigation tree including the **Kubernetes** section.

![](<../../../.gitbook/assets/env-k8s-step-02.png>)

### Step 2 — Namespaces List

In the sidebar, expand **Kubernetes** and click **Namespaces**. The list shows all namespaces provisioned under this resource group with their roles, service accounts, IAM role binding, and status. When starting fresh the list is empty. Click **+ Create Namespace** to begin.

![](<../../../.gitbook/assets/env-k8s-step-03.png>)

### Step 3 — Create Namespace

The **Create Namespace** form opens. Fill in:

* **Name** — a DNS-1123 compliant identifier (lowercase letters, digits, and hyphens; max 63 chars). For example `prod-namespace`.
* **Description** — optional

The form explains what will be provisioned: a Kubernetes namespace under this Resource Group with a read-only and a read/write service account, both bound to the resource group's IAM role via IRSA.

Click **Create & Provision**.

![](<../../../.gitbook/assets/env-k8s-step-04.png>)

### Step 4 — Namespace Provisioning Started

A success banner confirms **"Namespace 'prod-namespace' provisioning started"**. The namespace detail page opens with **Status: Provisioning**, showing the linked Resource Group ID and Environment ID. Click **Track Provisioning Status** to follow the agent.

![](<../../../.gitbook/assets/env-k8s-step-05.png>)

### Step 5 — Agent: Credentials & kubectl Setup

The agent opens a ticket titled **Namespace Resource Management — prod-namespace** using the `duplo-kubernetes-infra` skill. It begins by reading the task file to locate the namespace handler, sets up AWS credentials, and locates the `kubectl` and kubeconfig scripts needed to communicate with the EKS cluster.

![](<../../../.gitbook/assets/env-k8s-step-06.png>)

### Step 6 — Agent: Namespace Handler

The agent locates the correct task handler, reads the namespace spec, and runs the provisioning commands against the cluster. It creates the namespace and configures the two service accounts with their IRSA annotations.

![](<../../../.gitbook/assets/env-k8s-step-07.png>)

### Step 7 — Agent: Namespace Complete

Provisioning completes. The agent returns a summary of what was provisioned:

| Service Account | ClusterRole | Access | IAM Role ARN |
|---|---|---|---|
| `prod-namespace-readonly` | view | Read-only | `arn:aws:iam::813590939111:role/duplo-rb-prod-environment-prod-resourcegroup-1` |
| `prod-namespace-readwrite` | edit | Read/write | `arn:aws:iam::813590939111:role/duplo-rb-prod-environment-prod-resourcegroup-1` |

Both service accounts are annotated for IRSA so any pod in the namespace can assume the resource group's IAM role.

![](<../../../.gitbook/assets/env-k8s-step-08.png>)

### Step 8 — Namespace Ready

The namespace detail page updates to **Status: Ready**. The Overview tab confirms the namespace name and displays the service-account role bindings table with both accounts, their ClusterRole, access level, and IAM Role ARN. A footer confirms **"Namespace 'prod-namespace' provisioned"**.

![](<../../../.gitbook/assets/env-k8s-step-09.png>)

### Step 9 — Node Groups List

Click **Nodes** in the sidebar to open the Node Groups list. This page lists all EKS managed node groups under the resource group with their instance types, scaling configuration (min/desired/max), live status, and overall status. When starting fresh the list is empty. Click **+ Create Node Group** to begin.

![](<../../../.gitbook/assets/env-k8s-step-10.png>)

### Step 10 — Create Node Group: Basic Info

The **Create EKS Node Group** wizard opens. Fill in the Basic Info page:

* **Name** — used as the EKS node group name (e.g. `prod-nodegroup-1`)
* **Description** — optional
* **AMI Type** — automatically selected based on the cluster's Kubernetes version. For EKS 1.33 this defaults to `AL2023 x86_64 Standard`. Changing the AMI family re-filters the available instance types.
* **Instance Types** — select one or more from the available types in the region for the selected AMI architecture (e.g. `t3a.small`). Selecting multiple types improves availability.
* **Instance Visibility** — `Internal (private subnets)` places nodes in private subnets; `Public` places them in public subnets.

Click **Next**.

![](<../../../.gitbook/assets/env-k8s-step-11.png>)

### Step 11 — Create Node Group: Scaling & Config

Configure the scaling policy and storage:

* **Min Size** — minimum number of nodes (e.g. `1`)
* **Desired Size** — target number of nodes at creation (e.g. `2`)
* **Max Size** — maximum nodes the autoscaler can scale to (e.g. `3`)
* **Disk Size (GiB)** — root EBS volume size; minimum 20 GiB, encrypted gp3 (e.g. `50`)
* **Capacity Type** — `On-Demand` for stable workloads, `Spot` for cost savings on fault-tolerant workloads
* **Allocation Tag** — optional tag applied as `allocation-tag` on instances, volumes, and the node group; useful for cost allocation and chargeback reporting

Click **Create & Provision**.

![](<../../../.gitbook/assets/env-k8s-step-12.png>)

### Step 12 — Node Group Provisioning Started

A success banner confirms **"Node group 'prod-nodegroup-1' provisioning started"**. The node group detail page opens with **Status: Provisioning** and the spec summary:

* Resource Group: linked
* Capacity Type: ON\_DEMAND
* AMI Type: AL2023\_x86\_64\_STANDARD
* Disk Size: 50 GiB
* Instance Types: t3a.small
* Scaling: 1 / 2 / 3 (min/desired/max)

Click **Track Provisioning Status** to follow the agent.

![](<../../../.gitbook/assets/env-k8s-step-13.png>)

### Step 13 — Agent: Phase 0 & Phase 1

The agent opens a ticket titled **AWSEksNodeGroup Resource Management — prod-nodegroup-1** using the `duplo-kubernetes-infra` skill. It reads the `aws-eks-node-group` skill file, loads the spec, and runs Phase 0 (LOAD\_PROFILE guard) and Phase 1 (parameter validation). All fields are validated and the CloudFormation stack name is derived.

![](<../../../.gitbook/assets/env-k8s-step-14.png>)

### Step 14 — Agent: Variables Resolved

The agent exports all required shell variables — `WORKSPACE_ID`, `RESOURCE_ID`, region, VPC, subnet IDs, and node group configuration — and confirms validation passes. It then derives the stack name and checks for a pre-existing stack before proceeding to deployment.

![](<../../../.gitbook/assets/env-k8s-step-15.png>)

### Step 15 — Agent: CloudFormation Submitted

The AWS profile guard passes. The agent exports all session variables, submits the CloudFormation template for the EKS Managed Node Group, and enters Phase 4 — polling for stack completion. Stack events are streamed in real time as each resource is created.

![](<../../../.gitbook/assets/env-k8s-step-16.png>)

### Step 16 — Agent: Node Group Complete

The stack reaches `CREATE_COMPLETE`. Phase 5 collects full node group details and posts the final result. The completion summary confirms the node group name, ARN, CloudFormation stack, Kubernetes version, release version, instance type, scaling configuration, subnets, and final status.

![](<../../../.gitbook/assets/env-k8s-step-17.png>)

### Step 17 — Node Group Ready

The node group detail page updates to **Status: Ready**. The Details tab shows:

* **Node Group ARN** and **CloudFormation Stack ARN**
* **Kubernetes Version**: 1.33 / **Release Version**: 1.33.11-20268512
* **AWS Status**: ACTIVE
* **Autoscaling Group** name
* **Subnets**: the two private subnet IDs the nodes are placed in
* **Scaling**: 1 / 2 / 3 (min/desired/max)

Additional tabs — **Scaling**, **Nodes**, and **Health Issues** — provide live status of the autoscaling group and individual node health.

![](<../../../.gitbook/assets/env-k8s-step-18.png>)

### Step 18 — Workloads: Jobs

In the sidebar, expand **Kubernetes > Workloads** and click **Jobs** to see the Jobs list. The list shows all Kubernetes Jobs with their namespace, image, succeeded count, and status. Click **+ Create Job** to define a one-shot or batch workload.

![](<../../../.gitbook/assets/env-k8s-step-19.png>)

### Step 19 — Micro Services List

Click **Micro Services** in the sidebar to see all long-running application services (Deployments, StatefulSets, etc.) in this resource group. The list shows name, type, image, and status. When starting fresh the list is empty. Click **+ Create App Service** to deploy an application.

![](<../../../.gitbook/assets/env-k8s-step-20.png>)

### Step 20 — Add App Service: Workload Basics

The **Add App Service** wizard opens. Fill in the **Workload Basics** page:

* **Service Name** — DNS-1123 compliant name (e.g. `helloworld-application`)
* **Namespace** — auto-selected from the resource group's provisioned namespace (`prod-namespace`)
* **Docker Image** — the container image to run
* **Replicas** — number of pod replicas (e.g. `1`)
* **Allocation Tag** — optional cost allocation tag
* **Workload Type** — `Deployment` for stateless services; other options include StatefulSet, DaemonSet

The platform automatically attaches a read-only service account, resource group node selector, and resource tracking labels to every workload.

Click **Next**.

![](<../../../.gitbook/assets/env-k8s-step-21.png>)

### Step 21 — Pod Configuration

The **Pod Configuration** page configures pod-level scheduling and security. Two tabs are available:

* **Scheduling** — YAML editor for node affinity, pod anti-affinity, and tolerations. Insert snippets are provided for common patterns: **Required (linux)**, **Prefer spot nodes**, **Spread across nodes**, **Strict: 1 per node**, **Dedicated GPU**, and **Spot instances**.
* **Security & Other** — security context and other pod-level settings

Leave blank for a standard deployment and click **Next**.

![](<../../../.gitbook/assets/env-k8s-step-23.png>)

### Step 22 — Environment Variables

The **Environment Variables** page configures environment variables for the main container. Two tabs are provided:

* **ENV** — inline variables; insert snippets for **Key/Value** literals or **Field Ref** (downward API)
* **ENV from** — bulk import from a **SecretKeyRef** or **ConfigMapKeyRef**

Leave blank if no environment variables are needed and click **Next**.

![](<../../../.gitbook/assets/env-k8s-step-24.png>)

### Step 23 — Container Configuration

The **Container Configuration** page configures resources, ports, probes, and volume mounts for the main container. Four tabs are available:

* **Resources & Ports** — CPU/memory limits and requests; port definitions. Insert snippets: HTTP 8080, HTTPS 8443, Metrics 9090, and resource presets (1 CPU/1Gi, Medium workload).
* **Probes** — liveness and readiness probe configuration
* **Volumes & Mounts** — volume mount definitions
* **Other** — additional container settings

Leave blank for default resource limits and click **Next**.

![](<../../../.gitbook/assets/env-k8s-step-25.png>)

### Step 24 — Extra Containers

The **Extra Containers** page adds init containers or sidecar containers alongside the main container. Two tabs are provided:

* **Init Containers** — run to completion before the main container starts. Insert snippets: **Wait for TCP port**, **Wait for HTTP**, **DB Migration**.
* **Sidecar Containers** — run alongside the main container for the lifetime of the pod.

Leave blank if no auxiliary containers are needed and click **Next**.

![](<../../../.gitbook/assets/env-k8s-step-26.png>)

### Step 25 — Load Balancer

The **Load Balancer** page configures the Kubernetes Service and optional Ingress for this workload. Click **+ Add Port** to define a port mapping, or leave blank to skip external exposure. Service annotations and labels can be edited via **Edit** under SERVICE SETTINGS.

Click **Save & Provision** when ready.

![](<../../../.gitbook/assets/env-k8s-step-27.png>)

### Step 26 — Add Port

The **Add Port** modal configures how the service is exposed:

* **Service Type** — `ClusterIP` (internal), `NodePort`, or `LoadBalancer`
* **Container Port** — the port the container listens on (e.g. `80`)
* **Service Port** — the port exposed on the service (defaults to the container port)
* **Protocol** — `TCP` or `UDP`
* **Enable Ingress** — toggle on to create an ALB Ingress rule for this port
  * **Certificate** — select an ACM certificate from the plan (e.g. `*.salesdemo-apps.duplocloud.net`)
  * **Load Balancer Visibility** — `Public` or `Internal`
  * **Host** — auto-populated from the service and resource group name
  * **Path** — URL path prefix (e.g. `/`)
  * **Path Type** — `Prefix` or `Exact`

Click **Add Port**, then **Save & Provision**.

![](<../../../.gitbook/assets/env-k8s-step-28.png>)

### Step 27 — App Service Ready

The app service detail page opens with **Status: Ready**. The Overview tab shows the full deployment summary:

* **Namespace**: `prod-namespace`
* **Workload**: `helloworld-application`
* **Service**: `helloworld-application`
* **Ingress**: `helloworld-application`
* **Replicas Ready / Available**: 1 / 1
* **Service Type**: ClusterIP
* **Cluster IP**: `172.20.25.167`

The **Running pods** table lists each pod with its name, status, restart count, pod IP, and node. A **Diagnose** button provides quick access to pod logs and health checks.

![](<../../../.gitbook/assets/env-k8s-step-29.png>)

### Step 28 — Load Balancer Provisioned

After a few minutes the ALB finishes provisioning. The **Load balancer** section of the Overview tab populates with the hostname:

```
k8s-prodname-hellowor-e9cc394637-1380267796.us-east-1.elb.amazonaws.com
```

The application is now accessible via HTTPS through the ALB using the configured certificate and ingress path.

![](<../../../.gitbook/assets/env-k8s-step-32.png>)

## Next step

Once your workload is running, proceed to [Step 6: Add Databases](step-6-databases.md).
