# Installation

DuploCloud AI Suite is installed directly into your cloud account, running inside a Kubernetes cluster that you own and control. This document explains what you need to provide to DuploCloud, what we will set up, and what prerequisites your environment needs to meet before installation begins.

---

## How Installation Works

DuploCloud deploys the AI Suite into your cloud environment using a Helm chart. We manage the deployment process on your behalf — you do not need to run any commands yourself. Once the prerequisites are in place and access is granted, our team handles the installation end-to-end.

---

## Supported Cloud Providers

DuploCloud AI Suite runs on any of the following managed Kubernetes platforms:

| Cloud | Kubernetes Service | Guide |
|---|---|---|
| **AWS** | Amazon EKS | [AWS Installation](aws-installation.md) |
| **Google Cloud** | GKE | [GCP Installation](gcp-installation.md) |
| **Azure** | AKS | [Azure Installation](azure-installation.md) |

---

## What You Need to Provide

### 1. An AWS Account (or Existing Cluster)

The simplest path is to provide DuploCloud with a **fresh, dedicated AWS account**. Our team will create all required infrastructure — VPC, Kubernetes cluster, storage, certificates — from scratch with no risk of disrupting existing workloads.

If you already have a Kubernetes cluster and prefer to install into an existing account, that is fully supported. DuploCloud deploys into a dedicated namespace and does not modify any resource that was created outside of Duplo.

- **AWS:** Amazon EKS (existing cluster, or we create one)
- **GCP:** GKE (existing cluster required)
- **Azure:** AKS (existing cluster required)

### 2. Cloud Infrastructure

Depending on your cloud provider, the following infrastructure must be provisioned in your account before installation:

#### AWS (EKS)

| Resource | Purpose |
|---|---|
| **AWS Load Balancer Controller** | Routes external traffic to the application |
| **EFS Filesystem** | Shared file storage for the backend (mount targets in each node subnet) |
| **EFS CSI Driver** | Connects the cluster to EFS |
| **ACM Certificate** | TLS for the application domain |
| **IRSA Role** | IAM role for the backend service account with EFS permissions |

#### Google Cloud (GKE)

| Resource | Purpose |
|---|---|
| **Ingress Controller** | Routes external traffic (nginx or GKE built-in) |
| **Filestore CSI Driver** | Shared file storage for the backend |
| **Workload Identity** | Grants the backend service account access to storage |

#### Azure (AKS)

| Resource | Purpose |
|---|---|
| **Ingress Controller** | Routes external traffic (nginx or Azure Application Gateway) |
| **Azure Files CSI Driver** | Shared file storage for the backend (built-in on AKS ≥ 1.21) |
| **Azure Workload Identity** | Grants the backend service account access to storage |

### 3. A Domain Name and TLS Certificate

You must provide:
- A domain name (or subdomain) where the application will be hosted, e.g. `ai-helpdesk.yourcompany.com` — does not need to be publicly accessible; a private hosted zone is supported
- A valid **TLS certificate** for that domain (ACM on AWS, or cert-manager/Let's Encrypt on GCP/Azure)

### 4. Administrator Email Addresses

Provide a list of email addresses that should have **super-admin access** to the platform. These users will have full administrative control and can manage other users after installation.

---

## What DuploCloud Installs

Once the prerequisites are in place, DuploCloud deploys the following into your cluster:

| Component | Description |
|---|---|
| **Backend** | ASP.NET Core API server that powers the AI HelpDesk, project management, and agent orchestration |
| **Frontend** | React web application served via nginx — this is the UI your team interacts with |
| **MongoDB** | Embedded database (Kubernetes StatefulSet) for storing tickets, projects, reports, and configuration |
| **Web Terminal** | Browser-based terminal integration for agent command execution |
| **Duplo Agent** | Claude-powered AI agent runtime |
| **MCP Server** | Model Context Protocol server for tool integrations |
| **Ingress** | Load balancer / ingress resource routing HTTPS traffic to the application |
| **Persistent Storage** | Shared file volume (EFS / Filestore / Azure Files) mounted into the backend for storing agent working directories and generated artifacts |

All components run inside a dedicated namespace in your cluster and are fully contained within your cloud account. DuploCloud does not operate any shared infrastructure on your behalf — your data stays in your environment.

---

## Access DuploCloud Requires

To perform the installation, our team needs admin-level access to your AWS account and Kubernetes cluster.

The recommended approach is to create a dedicated IAM user with `AdministratorAccess` and share the credentials with DuploCloud. Admin access is required to create the VPC, EKS cluster, EFS, load balancer, and supporting resources. After installation is complete, the IAM user can be deleted.

For full details on granting access, see the [AWS Installation guide](aws-installation.md).

---

## After Installation

Once the deployment is complete, DuploCloud will provide:

- The **application URL** where your team can log in
- Confirmation that all services are healthy
- Onboarding guidance for creating your first workspace, inviting users, and configuring AI agents

For questions about the installation process, contact your DuploCloud account team.
