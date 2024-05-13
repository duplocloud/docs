---
description: Popular and frequently asked questions about DuploCloud
---

# FAQs

## What support features are included with my DuploCloud subscription&#x20;

See [DuploCloud Support](getting-started/duplocloud-support-model.md) for examples of what we do and do not support and how to contact us.

## What cloud providers does DuploCloud support?

DuploCloud supports the following:

* Amazon AWS
* Microsoft Azure
* Google Cloud
* On-Premises

Use these FAQ documents to quickly find answers to popular questions about using AWS, Azure, and GCP with DuploCloud.

{% content-ref url="aws-user-guide/aws-faq.md" %}
[aws-faq.md](aws-user-guide/aws-faq.md)
{% endcontent-ref %}

{% content-ref url="azure-user-guide/azure-faq.md" %}
[azure-faq.md](azure-user-guide/azure-faq.md)
{% endcontent-ref %}

{% content-ref url="gcp-user-guide/gcp-faq.md" %}
[gcp-faq.md](gcp-user-guide/gcp-faq.md)
{% endcontent-ref %}

## How much will DuploCloud add to my company's cloud spend?

We estimate that DuploCloud will increase your company's cloud costs by approximately $100 to $200 per month.

## General FAQs

### Can companies with private clouds use DuploCloud?

Yes, DuploCloud's On-prem services support companies with private clouds.&#x20;

### Is DuploCloud a SaaS product?

No. DuploCloud is a self-hosted solution deployed within the customer's cloud account. This hosted solution provides the customer with a SaaS-like experience. DuploCloud can provide a fully managed service to maintain uptime, provide updates, and supply ongoing support.

### What happens during the DuploCloud onboarding process?

1. DuploCloud creates a private Slack channel so your organization can communicate directly with the DuploCloud Support Staff to resolve any issues and answer questions during onboarding.
2. Typically clients create a separate AWS account, GCP project, or Azure subscription for DuploCloud, so we don't interfere with any pre-existing AWS accounts and configurations. The goal is to set up a development environment that the client team validates and switches over to, followed by staging and, finally, a Production migration. DuploCloud can also be integrated into an existing environment, or there can be a hybrid where some infrastructure is moved over to a DuploCloud-managed environment that connects to the existing environment.
3. DuploCloud installs the DuploCloud Portal for you and then schedules a call to orient you to the Portal and do additional configuration, such as creating DuploCloud Services, as required.
4. During the initial call with DuploCloud, you have the option of completing the set-up yourself, with help from our engineers. You can also create some Services and let our engineers set up the rest for you.
5. After your DuploCloud Portal has been installed and configured, DuploCloud Infrastructures (VPCs) are running, Kubernetes has been enabled and configured, and logging, monitoring, alerting, CI/CD, and Soc2 Controls have been implemented.

Even though the onboarding process can take thirty to seventy (30-70) hours, the DuploCloud staff performs about 90% of the work for you. Feel free to contact our Support staff anytime with questions or concerns.

In addition, during setup, we perform penetration testing and vulnerability assessments for your applications. Using our SIEM solution, we assess the vulnerabilities of DuploCloud Hosts in the Infrastructure.

### How is DuploCloud Portal accessing my cloud infrastructure, and how is it secured?

DuploCloud is a self-hosted single-tenant solution deployed within the customer's cloud account. The software runs in a virtual machine (VM), and the VM derives permissions to call the cloud provider using the VM's permissions. Specifically, in AWS, DuploCloud utilizes an IAM role, known as an instance profile, to access AWS accounts, ensuring secure access without needing access keys. In Azure, permissions are derived via managed identity and service accounts in GCP.

### Multi-AWS Account Setup with DuploCloud

For those looking to manage workloads across multiple AWS accounts, it's necessary to install a DuploCloud appliance in each account. This ensures effective management of the workloads in different environments, aligning with DuploCloud's comprehensive support for multi-cloud and hybrid cloud setups.loud Portal are secured, as is any other workload in the cloud. In addition to SSO login for portal access, the VM runs optionally behind a VPN. Therefore, only internal users can load the portal when connected to a VPN.

### Can we install DuploCloud in our existing cloud account?

While you can install DuploCloud in your existing environment, we prefer that we do the setup in a separate account. This does not mean you must migrate all your existing data sources, especially if you have terabytes of files in the S3 bucket. The workload in DuploCloud environments can connect to existing data sources and endpoints over peering and cross-account access. Here are the top reasons why people prefer Duplocloud in a separate account:

* It is considered a very safe and non-intrusive way to validate the new setup and, at times, new architecture, like Kubernetes, without touching the existing account.
* From a compliance perspective, a new account is a clean slate and is very easy to pass audits as DuploCloud will guarantee all aspects of it. If we were to fit in an existing account, there may be many things that are quite hard and, in some cases, impossible to fix. For example, if things were operated non-compliantly, that history is stored in a cloud trail. This can indicate irregularities to an auditor and creates a lot of questions around scope, leading to exceptions in the report.
* Some DuploCloud security features can impact existing non-compliant resources and workloads. While this is rare, it is something to consider.

In summary, while one can deploy the platform in an existing account, even import a VPC and Kubernetes clusters, avoiding it can cause more overhead than benefit than a new account with either data migrated or connected to existing data sources over cross-account access.

### Am I locked into DuploCloud? If so, what work do I need to do to move away from it?

DuploCloud is running in your own cloud account, along with your workloads. DuploCloud is a provisioning system, so stopping DuploCloud does not impact any of your applications and cloud services.

The following is a list of automation constructs managed by DuploCloud and a summary of what you need to do to maintain them directly instead of through DuploCloud.

1. Cloud Provider Configuration (Terraform): This involves various cloud services, IAM roles, Security groups, VPC, etc. DuploCloud can export your latest cloud configuration into native Terraform code and state files. Once exported, you maintain the configuration.
2. Kubernetes: All applications and configurations that have been deployed in K8s are available in the form of deployments, StatefulSets, DaemonSet, K8s Secrets, ConfigMaps, etc. One can run `kubectl`commands to export configurations as YAML files and continue to maintain them in the future.
3. Compliance monitoring: DuploCloud uses a third-party SIEM solution called [Wazuh](https://www.wazuh.com). Wazuh is an open-source software platform running in an independent VM in your cloud account, and you have full permission to retain it "as-is." However, going forward, you need to integrate any new systems that need compliance monitoring into the SIEM.
4. Diagnostics tools: These include Prometheus, Grafana, and Elasticsearch. They are all open source and run in your cloud account, so you can continue to manage them directly.

{% hint style="info" %}
If DuploCloud is down, it's similar to having an unavailable DevOps engineer. If you need to opt out of DuploCloud, you are replacing your DevOps management. DuploCloud is neither a PaaS nor a hosted solution that hosts your workloads.
{% endhint %}

### Our company has no DevOps experience. Can DuploCloud provide services to build our environment and support us?

Absolutely! More than half of our customers have no DevOps team. With our managed service offering, we handle your deployments, act as the first line of defense for any issues, and are constantly involved in daily tasks like CI/CD updates.

The DuploCloud team is your extended DevOps team, assisting with white glove environment setup and daily operations with 24x7 Slack and email support. We cover what is supported in the DuploCloud platform and assist with your cloud provider's requirements.

After the initial onboarding of the platform, we recommend that you engage the DuploCloud team as your second line of defense by setting up an internal triage process of your own. We can assist you in setting up this process.

{% hint style="info" %}
DuploCloud is your extended DevOps team! We are available 24x7 on your Slack channel, by phone, and by email.
{% endhint %}

### Can I make changes directly in the cloud account managed by DuploCloud?

Yes. This is often required because DuploCloud may not support all cloud features or configurations. Direct changes to your cloud account can be categorized within the following groups:

#### Independent Changes

DuploCloud labels the resources and configurations it manages. If independent changes are being made directly with your cloud provider, DuploCloud will not interfere. However, DuploCloud still monitors changes for compliance and alerts you to non-compliant configurations.

#### Non-conflicting changes to DuploCloud managed resources

For resources that DuploCloud does not manage directly, you change directly in your cloud provider. For example, if you add additional forwarding rules to a load balancer created through DuploCloud, DuploCloud does not interfere with the new configuration that you created.

#### Conflicting Changes to DuploCloud-managed resources

For resources that DuploCloud manages, DuploCloud automatically detects conflicts and either revert changes or raises an alert about inconsistencies.

{% hint style="info" %}
DuploCloud provides flexibility when a feature that is not supported by DuploCloud can be programmed directly in your cloud provider. If you are using Terraform, then the DuploCloud provider and the native cloud provider can be used in tandem. For an example of this use case, see [https://duplocloud.com/white-papers/devops/#PAAS](https://duplocloud.com/white-papers/devops/#PAAS).
{% endhint %}

### I don't know IaC (Infrastructure-as-Code). Can I still use DuploCloud?

Yes. DuploCloud's Web UI is a no-code interface for DevOps. You do not need to know IaC or have cloud expertise to operate it. However, you should read the product documentation to understand the basic constructs in DuploCloud.

### Isn't No Code Click Ops?

"Click Ops" is when engineers manually create infrastructure resources in the cloud and other UIs. It's often considered bad practice because there are so many components and configurations that it's easy to make mistakes. You can skip past default settings that aren't secure, copy configuration incorrectly between environments, etc. You need hundreds or thousands of clicks and a lot of DevSecOps knowledge.

DuploCloud manages infrastructure resources for you. You pick application-level functionality like "services" and "load balancers," then, DuploCloud creates the complex cloud resources needed to deliver that functionality. It ensures the underlying compute instances, firewall rules, IAM policies, and other components are configured following good practices. You only need a few clicks and don't need to know DevSecOps because DuploCloud knows it for you.

Click Ops is an easy way to make mistakes. DuploCloud's No Code is an easy way to ensure you don't.

### **Should I use low-code or no-code?**

The answer depends on the following key factors:

#### How much Developer self-service do you require?

Especially in a rapidly growing company environment, where architecture is constantly evolving and services are constantly updated, there may be a desire to let developers self-service and move fast. This would be a case for no-code. On the other hand, in cases where there is an established operations organization with centralized requirements, a low-code Terraform solution may be a better option.

Note that Terraform is a client-side scripting tool and a single-user system, so the scope of a project is limited to one person operating at one time. This can incur constraints if a project has many components and two people cannot operate simultaneously, even if they deal with completely independent constructs.

#### Dealing with a broad scope of changes vs. small, Just-In-Time changes

Terraform projects typically have a broad scope with multiple components. Sometimes, you must make small targeted changes (for example, a health check URL change). But when the change is being executed, there may be other drifts, and the user may be forced to resolve them. This can be inconvenient, and often, the user will change the UI, resulting in further configuration drifts.

{% hint style="info" %}
About half of our customer base uses no-code, while the other half uses Terraform. Ironically, software developer-centric companies prefer no-code because it enables engineers to be agile and focus on their application code. By contrast, the low-code Terraform provider is often used in DevOps-centric organizations.
{% endhint %}

### How is the DuploCloud subscription cost calculated?

DuploCloud license usage is calculated based on the services managed by DuploCloud. The service usage is counted in terms of units, with a unit defined as below:

* A host is counted as 1 unit. (example: EC2 instance, Azure, or GCP VM)
* A serverless function or service is counted as 1/4 unit (example: Lambda function)
* A serverless application is counted as 1/2 unit (example: AWS ECS Service, Azure Web App, Google GKE Service)
* AWS Managed Airflow (MWAA) worker is counted as 1/2 unit. For an MWAA environment, the number of workers is calculated as the average of the minimum and maximum worker count.

### Can you delete an application and all its resources with a single click and confirmation?

Yes.

### Can anything in the UI be automated over an API as well?

Yes. Every element in the DuploCloud UI is populated by calling an API.

### Does DuploCloud make any assumptions we should be aware of that may impact initial implementation time?

No. DuploCloud segregates resources into environments called Tenants, which accelerates ramp-up time. For more information about implementation,[ contact the DuploCloud support team](https://duplocloud.com/company/contact-us/).

## Connectivity and Availability FAQs

### I can't edit the Service Description to update my control plane configuration.

You must make control plane modifications before [enabling central logging](aws-user-guide/use-cases/central-logging/central-logging-setup.md). If logging is enabled, the Service Description cannot be edited.

### How do you create a Host with a public IP?

While creating a Host, click on Show Advanced to display advanced options and select the public subnet from the list of availability zones.

### How do I SSH into the host?

Under each Host, you can click on Connection Details under the Actions dropdown, which will provide the key file and instructions to SSH.

### My host is Windows. How do I use RDP (Remote Desktop Protocol)?

Under Host, click on Connection Details under the Actions dropdown. It will provide the password and instructions on how to connect to RDP.

### How do I get into the container where my code is running?

Under the Services Status tab, find the host where the container is running. SSH into the host (see instructions above), and run `sudo docker ps` to get the container ID. Next, run `sudo docker exec -it`_**`CONTAINER_ID`**_`bash`. Find your container using the image ID.

### I cannot connect to my service URL. How do I debug it?

Make sure the DNS name is resolved by running `ping` on your local machine. Ensure that the application is running running `ping` from within the container. SSH into the host, and connect to your Docker container using the Docker exec command `sudo docker exec -it`_**`CONTAINER_ID`**_`bash`. From inside the container, curl the application URL using the IP 127.0.0.1 and the port where the application is running. Confirm that this works. CURL the same URL using the container's IP address instead of 127.0.0.1. The IP address can be obtained by running the `ifconfig` command in the container.

If the connection from within the container works, exit the container and navigate to the host. Curl the same endpoint from the host (i.e., using container IP and port). If this works, then under the ELB UI in DuploCloud, note down the host port that DuploCloud created for the given container endpoint. This will be in the range of 10xxx or the same as the container port. Now try connecting to the “HostIP,” and DuploMappedHostPort just obtained. If this also works but the service URL fails, contact your enterprise admin or duplolive-support@duplocloud.net.

## Kubernetes FAQs

### Is Kubernetes required to use DuploCloud? Is using Kubernetes better than using ECS?

No, Kubernetes is not required. DuploCloud supports both AWS ECS and Kubernetes, among other Cloud solutions.

The main advantage of Kubernetes is its broad-based, highly customizable, third-party, open-source community that champions and supports it as a delivery platform. For example, Astronomer (managed air flow), Time series database, IsTio Service Mesh, and Kong API Gateway all expect you to have a Kubernetes deployment. However, if your business needs and use cases are met with an AWS solution, you may not need Kubernetes.

Choose the container management software that best meets your use cases and requirements' complexity level. DuploCloud supports AWS, Kubernetes, Azure, and GCP. Many customers use software from multiple vendors to create robust business solutions backed by DuploCloud's compliance assurance and automated low-code/no-code DevOps approach.

### I want to have multiple replicas of my MVC (Model-View-Controller) service. How do I make sure that only one of them runs migration?

Enable Health Check for your service and ensure the API does not return HTTP 200 status until migration is done. Since DuploCloud waits for a complete Health Check on one service before upgrading to the next service, only one instance will run migration at a time.

## Upgrade FAQs

### What is a rolling upgrade, and how do I enable it?

When you update (e.g., change an image or ENV variable) a service with multiple replicas, DuploCloud makes the change to one container at a time. If an updated container fails to start or the health check URL does not return HTTP 200 status, DuploCloud will pause the upgrade of the remaining containers. This can typically be remedied by updating the service with a newer image with a fix. If no health check URL is specified, DuploCloud only checks to see if an updated container is running before moving on to the next. To specify Health Check, use the Elastic Load Balancer menu to find the Health Check URL suffix.

## Container/Docker FAQs

### One or more of my containers are pending. How can I debug?

If the current status is Pending and the desired status is Running, wait a few minutes for the image to finish downloading. If it’s been more than five minutes, check the faults from the button below the table. Ensure that your image name is correct and does not have spaces. Image names are case-sensitive, so they should be all lowercase, including the image name in DockerHub.

If the current state is Pending when the desired state is Delete, the container is the old service version. It is still running because the system is being upgraded, and the previous replica has not been upgraded yet. Check the faults in other containers of this service for which the Current State is Pending and the desired state is Running.

### Some of my container statuses say “pending delete.” What does this mean?

A Pending Delete status indicates that DuploCloud intends to remove these containers, indicating that a system update or service upgrade is in progress. This status often appears during rolling upgrades, where DuploCloud systematically replaces old container versions with new ones to ensure service continuity and minimal downtime. The most common cause is that DuploCloud blocked the upgrade because a replica of the service was upgraded but is no longer operational. Some replicas may show a Running status even though the Health Check failed and the rolling upgrade is blocked. To unblock the upgrade, restore the service configuration (image, environment, etc.) to an error-free state.

## Error Messages

### I'm receiving the error message `Could not load credentials from any providers`.

Your `duplo-jit` local cache must be cleared. To do this, run the following command:

```bash
rm -rf ~/Library/Caches/duplo-jit/
```

### When creating a Service, I'm receiving the DuploCloud Fault `Conditions Unschedulable because 0/N nodes are available: 1 node(s) didn't match pod anti-affinity rules, 1 node(s) were unschedulable....`

Two possible reasons for receiving this fault message are:

* You are not allocating enough hosts to process your workload.
* The [allocation tags](gcp-user-guide/container-deployments/concepts.md#allocation-tags) you assigned to your existing Hosts limit additional Service workloads.

### I do not see logs displayed for a Tenant. I get the error `Docker native collection agent Filebeat is not running for Tenant`.

Ensure that [logging is set up](aws-user-guide/use-cases/central-logging/central-logging-setup.md) and that you have selected the Tenant for which you want to collect logging information.

## Terraform FAQs

### Is DuploCloud generating Terraform code behind the scenes to configure the cloud?

No. DuploCloud calls the cloud provider's API directly. Based on user requirements, the software interacts with the cloud provider API asynchronously, maintaining a state machine of operations with built-in retries to ensure robustness. Interacting with the cloud provider continuously monitors any configuration drift, system faults, security, and compliance controls.

### If DuploCloud is not generating Terraform code behind the scenes, how can I use Infrastructure-as-code?

The Terraform and DuploCloud Web UIs are layered on top of the DuploCloud platform.

![User Interaction with the DuploCloud Platform](<.gitbook/assets/image (11) (1) (1).png>)

DuploCloud provides an SDK into Terraform called the [DuploCloud Terraform Provider](https://registry.terraform.io/providers/duplocloud/duplocloud/latest). This SDK allows users to configure their cloud infrastructure using DuploCloud constructs rather than lower-level cloud provider constructs. This enables the user to get the benefits of Infrastructure-as-Code while significantly reducing the needed code. The DuploCloud Terraform Provider calls DuploCloud APIs. Our [DevOps white paper](https://duplocloud.com/white-papers/devops) provides detailed examples.

### **If my developers make changes via the DuploCloud UI, what happens to the Terraform code my DevOps engineers have written?**

You should create a separation between your developers and your DevOps team. Allowing developers to use the Web UI in non-production development environments to quickly iterate product changes can create inconsistency.

In both production and critical non-production environments, the cloud services setup and first-time application deployment can be done via Terraform code. CI/CD workflows can be built that only update the application (Docker and Lambda) deployments. The DevOps team should do any cloud service level change via Terraform, and developers should ask the DevOps team to do the same. Developers should still be able to trigger CI/CD for their application rollouts without DevOps involvement.

## Security and Compliance FAQs

### How can I set up Multi-Factor Authentication (MFA) for OpenVPN authentication?

From the DuploCloud portal, click on your name in the top right corner and select Profile. Click on the VPN URL and enter the required credentials. On the first login, scan the barcode displayed on the screen. Download the profile, and add it to the OpenVPN Connect. The next time you log in with OpenVPN, you will be prompted to enter the authentication code.&#x20;

## CI/CD FAQs

### How does CI/CD work with DuploCloud?

CI/CD is the topmost layer of the DevOps stack. DuploCloud should be viewed as a deployment and monitoring solution invoked by your CI/CD pipelines, written with tools such as CircleCI, Jenkins, GitHub Actions, etc. You build images and push them to container registries without involving DuploCloud, but you invoke DuploCloud to update the container image. An example of this is in the CI/CD section. DuploCloud offers its own CI/CD tool.

## Diagnostic Tool FAQs

### How do I use Datadog and other diagnostics tools?

DuploCloud's out-of-the-box diagnostics stack is optional. To integrate with a third-party toolset like Datadog, you follow the toolset's guidelines and deploy collector agents. You can do this as if you are running an application within the respective DuploCloud tenants.
