---
description: Use Cloud Deploys in the DevKit to publish your own DuploCloud portal in your cloud account, step by step.
---

# Deploy Your Portal to Your Cloud

Cloud Deploys is an agent in the DevKit that publishes your own DuploCloud portal in **your** cloud account. You pick a connected cloud provider and answer a short wizard. You review exactly what will be created, then approve it. When it finishes, Cloud Deploys gives you the portal URL.

{% hint style="info" %}
**Cloud Deploys is in preview.** It is not released yet, and the screens and steps on this page may change. AWS is the only cloud available today. Azure and Google Cloud appear in the wizard as **Coming soon**.
{% endhint %}

DuploCloud may also deploy the portal for you, case by case. If you would rather not run the wizard yourself, ask your DuploCloud contact.

If you already run Kubernetes and want to install the portal with Helm yourself, use the [Systems Integrator Installation Guide](systems-integrator-installation-guide.md) instead.

***

## What you need first

| Requirement | Details |
| --- | --- |
| **The DevKit** | Running on your machine, with Cloud Deploys loaded. See [Install the DevKit](../install-the-devkit.md). |
| **A license** | The wizard registers a license for your portal's URL. By default it reuses your DevKit license. You can also paste a license token from the [DuploCloud Console](https://console.duplocloud.com). See [License](../licensing.md). |
| **A connected cloud provider** | An AWS provider attached to your workspace, with permission to create and manage VPC, EKS, IAM, S3, EFS, ACM and Route 53 resources. See [Amazon Web Services (AWS)](../integrating-providers/amazon-web-services-aws.md). |
| **A DNS zone or an existing certificate** | Either a Route 53 hosted zone that contains your portal's hostname, or an ACM certificate that covers it. You can also use a different DNS provider and add the records yourself. |
| **Outbound HTTPS** | The DevKit must reach GitHub (to download OpenTofu once), `registry.opentofu.org` (provider downloads), your cloud's APIs and the DuploCloud Console. |

Nothing is created in your account until you review a plan and approve it.

Cloud-specific details are on the per-cloud pages: [AWS](aws-installation.md), [Azure](azure-installation.md) and [Google Cloud](gcp-installation.md).

***

## Deploy your portal

Open **Cloud Deploys** in the DevKit menu and start a new deployment. The wizard takes you through these steps in order. The left rail shows your progress and your answers so far.

| Step | What you do |
| --- | --- |
| **1. Cloud** | Choose **Amazon Web Services**. Azure and Google Cloud are disabled and marked **Coming soon**. |
| **2. Provider** | Choose one of the AWS providers attached to your workspace. The wizard connects to the account and shows the account ID. If none is listed, add a provider, then refresh. |
| **3. Deployment** | Enter a **Deployment name**, an optional description and the **AWS region**. Everything is created in that region. |
| **4. Network** | Create a new VPC (recommended) or use an existing one. |
| **5. Cluster** | Create a new EKS cluster (recommended) or use an existing one. Set the Kubernetes version, worker instance type and node counts. |
| **6. Storage** | Create or reuse an EFS file system and S3 bucket. |
| **7. DNS & certificate** | Enter the portal URL and terminal URL, and choose how DNS and the HTTPS certificate are handled. |
| **8. Cluster add-ons** | Install the add-ons the portal needs, or confirm that your cluster already has them. |
| **9. Helpdesk** | Choose how the first admin signs in and list the admin emails. |
| **10. License** | Get a license for your portal's URL automatically, or paste one. |
| **11. Review** | Check every answer, then save. |

{% hint style="info" %}
The deployment name must be 3 to 32 characters: lowercase letters, digits and dashes, starting with a letter. It names your Terraform state and your license environment, so it **cannot be changed later**.
{% endhint %}

Each step with an existing-resource option shows a dropdown of what Cloud Deploys finds in your account. See [Use your existing network or cluster](#use-your-existing-network-or-cluster).

### DNS and certificate

You choose one of three modes on the **DNS & certificate** step:

| Mode | What happens |
| --- | --- |
| **Route 53 (automatic)** | You pick a hosted zone. Cloud Deploys creates the certificate and its validation records, and creates the portal's DNS records for you. The portal URL must sit inside the zone you pick. |
| **Use an existing certificate** | You pick an ACM certificate that covers both hostnames. Nothing is created in DNS. After the deploy you create the final DNS records yourself. |
| **I'll use a different DNS provider** | Cloud Deploys creates the certificate only. You add the validation records and the final records at your DNS provider. |

With a different DNS provider, the deployment pauses after the infrastructure is created. It shows the validation records to add, then waits for you to confirm. Validation usually takes a few minutes and can take up to 45.

### First login

On the **Helpdesk** step, choose how the first admin signs in:

* **Admin email and password.** This is the default. The password must be at least 8 characters.
* **Google sign-in.** Enter your Google client ID and client secret.
* **Microsoft sign-in.** Enter your Microsoft client ID, tenant ID and client secret.

Use **Admin emails** to list everyone who should get full administrative access. Passwords and client secrets are not shown in the review or the logs.

### Review the plan

After you save, Cloud Deploys works out what it will create and shows it to you first. **Nothing changes in your account until you approve.** The deployment runs in two stages, and each has its own plan:

1. **Infrastructure plan.** The network, cluster, storage, certificate and DNS. Review it, then choose **Deploy infrastructure**.
2. **Application plan.** The add-ons and the portal itself, installed on your cluster. Review it, then choose **Deploy Helpdesk**.

If you change any answer after a plan, the plan is marked out of date and you review a new one. An apply always uses the plan you reviewed.

### Apply and finish

Each deploy runs inside the DevKit extension, not through an AI model. You can watch the live log and safely leave the page. When the second stage finishes, the page shows **Helpdesk is live** with your portal URL and how to sign in for the first time.

If the load balancer is still starting, the page says so. Choose **Refresh** after a few minutes. If you chose a different DNS provider, the page lists the DNS records to create at your provider.

If a run fails, the page shows what went wrong and nothing else happens until you choose what to do next. A failed apply is not retried. Fix the cause and review a new plan.

***

## What gets created

With the recommended options, Cloud Deploys creates these resources in your account:

| Resource | Purpose |
| --- | --- |
| **VPC** | Public and private subnets across three zones, with a NAT gateway |
| **EKS cluster and node group** | Runs the portal |
| **EFS file system** | Shared storage for agent working directories and generated files |
| **S3 buckets** | Files and user data |
| **ACM certificate** | HTTPS for the portal and terminal URLs |
| **Route 53 records** | Only in Route 53 mode |
| **Cluster add-ons** | AWS Load Balancer Controller, EFS CSI driver, external-dns (Route 53 mode only) and a storage class |
| **The portal** | The DuploCloud portal installed with its Helm chart in its own namespace, with IAM roles for its services |
| **A state bucket** | One S3 bucket per account holding the deployment's state |

The state bucket is private, versioned and encrypted. It also stores the details that let you [find and take over the deployment](#take-over-an-existing-deployment) later. Everything stays in your account.

***

## Use your existing network or cluster

Each infrastructure step offers an option to use something you already have instead of creating it: a VPC, an EKS cluster, an EFS file system, an S3 bucket, or the cluster add-ons. Resources you adopt are **used as-is and never modified**.

Cloud Deploys checks an adopted resource before it plans. A failed check blocks you with an explanation and a **Re-check** button. Some checks only warn.

| Resource | What is checked |
| --- | --- |
| **VPC** | The private subnets route to a NAT gateway, so worker nodes can reach the internet. |
| **EKS cluster** | The provider has cluster-admin access, and the cluster has an IAM OIDC provider. A warning appears if the cluster is in a different VPC from the one you chose. |
| **EFS file system** | It has mount targets in the private subnets you chose, and its security groups allow NFS (TCP 2049) from the cluster nodes. |
| **Cluster add-ons** | The `ai-studio-efs` storage class exists. Warnings appear if the load balancer controller, EFS CSI driver or external-dns is missing. |

***

## Take over an existing deployment

Each deployment records its details in the state bucket in your own account. That means you can manage it again after a DevKit reset, or from a colleague's DevKit.

1. Open **Cloud Deploys**. Under **Found in your cloud**, the DevKit lists deployments it finds in the accounts of your connected providers. Choose **Scan again** to refresh the list.
2. Choose **Manage** next to the deployment.
3. Choose **Check for changes**. Cloud Deploys compares what is running with what the deployment describes. Nothing changes until you approve.

Taking over does not register a new license. To stop managing a deployment from this DevKit without touching your cloud, choose **Stop managing**. To remove the infrastructure, choose **Destroy**.

***

## Other installation guides

* [Systems Integrator Installation Guide](systems-integrator-installation-guide.md): install the portal with Helm into a Kubernetes cluster you manage.
* [AI DevOps V1 to V2 Upgrade](v1-to-v2-upgrade.md): upgrade an existing installation.
