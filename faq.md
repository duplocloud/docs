---
description: Popular and frequently asked questions about DuploCloud
cover: .gitbook/assets/Linkedin-bannerV3 (1).png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# FAQs

Use these FAQ documents to quickly find answers to popular questions about using AWS, Azure, and GCP with DuploCloud.

{% content-ref url="aws-user-guide/aws-faq.md" %}
[aws-faq.md](aws-user-guide/aws-faq.md)
{% endcontent-ref %}

{% content-ref url="overview-2/azure-faq.md" %}
[azure-faq.md](overview-2/azure-faq.md)
{% endcontent-ref %}

{% content-ref url="gcp-user-guide/gcp-faq.md" %}
[gcp-faq.md](gcp-user-guide/gcp-faq.md)
{% endcontent-ref %}

## General FAQs

### What cloud providers does DuploCloud support?

* Amazon AWS
* Microsoft Azure
* Google Cloud
* On-Premises

### What support features come with my DuploCloud subscription?

See [DuploCloud Support](welcome-to-duplocloud/duplocloud-support-model.md) for examples of what we do and do not support and how to contact us.&#x20;

For more detailed inquiries or assistance, including DuploCloud's DevOps automation platform capabilities, compliance, AWS services like Kinesis stream, and product updates, refer to the [official documentation](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/) and [whitepapers ](https://duplocloud.com/white-papers/)available on DuploCloud's website.

### How much will DuploCloud add to my company's cloud budget?

We estimate that DuploCloud will increase your company's monthly cloud costs by approximately $100 to $200.

### How is the DuploCloud subscription cost calculated?

DuploCloud subscription cost is based on the services managed by the platform, with usage counted in units. Here is how units are defined:

* Each host (e.g., EC2 instance, Azure VM, or GCP VM) is 1 unit.
* Serverless functions or services (e.g., Lambda functions) are 1/4 units.
* Serverless applications (e.g., AWS ECS Service, Azure Web App, Google GKE Service) are 1/2 units.
* AWS Managed Workflows for Apache Airflow (MWAA) workers are 1/2 units, with the number of workers calculated as the average minimum and maximum worker count.

### Can companies with private clouds use DuploCloud?

Yes, DuploCloud's On-Premises solution supports companies with private clouds.

### Is DuploCloud a Software as a Service (SaaS) product?

No. DuploCloud is a self-hosted solution deployed within the customer's cloud account, providing the customer with a SaaS-like experience. DuploCloud's fully managed service maintains uptime, provides updates, and supplies ongoing support.

### What happens during the DuploCloud onboarding process?

* DuploCloud creates a private Slack channel for direct communication during onboarding.
* Clients (usually) set up separate AWS accounts, GCP projects, or Azure subscriptions to avoid interfering with existing setups. This creates a development environment for the team to test and transition to before proceeding to staging and production. DuploCloud can be integrated into your existing environment, or a DuploCloud-managed environment can be connected to your current setup in a hybrid arrangement.
* Our engineers install the DuploCloud Portal and schedule a call to orient you and complete any additional configurations. You can complete the setup at this time or create some services and let DuploCloud engineers handle the rest. We also perform penetration testing and vulnerability assessments on your applications and Infrastructures using our SIEM solution.
* Once your DuploCloud Portal is installed and configured, DuploCloud Infrastructures (VPCs) are operational; Kubernetes is enabled and configured; and logging, monitoring, alerting, CI/CD, and SOC 2 controls are implemented.

Although the onboarding process can take thirty to seventy (30-70) hours, DuploCloud staff performs about 90% of the work. Contact [DuploCloud Support](welcome-to-duplocloud/duplocloud-support-model.md) with any additional questions.

### How does the DuploCloud Portal access my cloud infrastructure, and how is it secured?

DuploCloud is a self-hosted single-Tenant solution deployed within the customer's cloud account. The software runs in a virtual machine (VM) that is granted specific permissions allowing it to interact with and manage your cloud resources. In AWS specifically, DuploCloud uses Identity and Access Management (IAM) roles and instance profiles to access AWS resources without access keys. In Azure, permissions derive from Managed Identity, and in GCP they derive from service accounts.

### Can we install DuploCloud in our existing cloud account?

While you can install DuploCloud in your existing environment, we prefer to do the setup in a separate account. You do not have to migrate all your existing data sources, especially if you have large files in resources like S3 buckets. DuploCloud environments can connect to existing data sources and endpoints via peering and cross-account access. Here are the top reasons why people prefer DuploCloud in a separate account:

* It is a safe and non-intrusive way to validate a new setup or architecture (like Kubernetes) without touching the existing account.
* From a compliance perspective, a new account is a clean slate. Existing accounts may have issues that are difficult or impossible to fix. For example, accounts with cloud trails showing past non-compliance can indicate irregularities and create questions around scope, which may impact an auditor's report.
* Some DuploCloud security features can affect existing non-compliant resources and workloads. While this is rare, it is something to consider.

In summary, while you can deploy DuploCloud in an existing account or import existing VPC and Kubernetes clusters, migrating or connecting your data to new accounts often requires less overhead and provides more benefits.

### Am I locked into DuploCloud? If so, what work must I do to move away from it?

DuploCloud is a provisioning system that runs along with your workloads in your cloud account. Stopping it does not impact your applications or cloud services.

The following is a list of automation constructs managed by DuploCloud and a summary of what you need to do to maintain them directly instead of through DuploCloud.

#### Cloud provider configuration (Terraform)

This involves various cloud services, IAM roles, security groups, VPCs, etc. DuploCloud can export your latest cloud configuration into native Terraform code and state files. Once exported, you maintain the configuration.

#### Kubernetes

All Kubernetes applications and configurations are available as deployments, StatefulSets, DaemonSets, Kubernetes Secrets, ConfigMaps, etc. You can run `kubectl` commands to export Kubernetes configurations as YAML files and continue to maintain them in the future.

#### Compliance monitoring

DuploCloud uses a third-party SIEM solution called [Wazuh](https://www.wazuh.com). Wazuh is open-source software running in an independent VM in your cloud account, and you have full permission to retain it "as-is." However, in the future, you would need to integrate any new systems that need compliance monitoring into the SIEM.

#### Diagnostics tools

These include Prometheus, Grafana, and Elasticsearch. They are all open source and run in your cloud account, so you can continue to manage them directly.

{% hint style="warning" %}
If DuploCloud is down, it's like having an unavailable DevOps engineer. Opting out of DuploCloud is like replacing your DevOps management. DuploCloud is neither a Platform as a Service (PaaS) nor a hosted solution.
{% endhint %}

### Our company has no DevOps experience. Can DuploCloud build our environment and support us?

Absolutely! More than half of our customers have no DevOps team. With our managed service offering, we handle your deployments, act as the first line of defense for any issues, and manage daily tasks like CI/CD updates. Our team manages your cloud infrastructure and ensures it's optimized and modernized following the latest industry best practices.

The DuploCloud team is your extended DevOps team. We provide white-glove assistance for environment setup and daily operations with 24x7 Slack and email support. We can help with anything the DuploCloud platform supports and your cloud provider's requirements. This includes everything from Infrastructure-as-Code improvements for reusability and code reduction to architecture refactoring or infrastructure modernization. For instance, DuploCloud engineers could guide you in transitioning from deploying your applications on VMs to using Kubernetes. However, it's important to note that DuploCloud does not refactor customer application code.

{% hint style="info" %}
DuploCloud is your extended DevOps team! We are available 24x7 on your Slack channel, by phone, and by email.
{% endhint %}

### Can I make changes directly in a DuploCloud-managed cloud account?

Yes. You will need to make direct changes in the cloud account for cloud features or configurations not supported by DuploCloud. Direct cloud account changes can be categorized into the following groups:

#### Independent changes

Independent changes are changes to non-DuploCloud-managed resources made directly in your cloud provider. DuploCloud does not interfere with independent changes but still monitors and alerts you to non-compliant configurations.

#### Non-conflicting changes to DuploCloud-managed resources

DuploCloud does not interfere with non-conflicting changes to the resources it manages. For example, if you add additional forwarding rules to a Load Balancer created in DuploCloud, DuploCloud will not interfere with the new configuration.

#### Conflicting changes to DuploCloud-managed resources

DuploCloud automatically detects conflicting changes to DuploCloud-managed resources and reverts changes or raises an alert about inconsistencies.

DuploCloud allows you to program unsupported features directly in your cloud provider. If you're using Terraform, you can use the DuploCloud provider and the native cloud provider together. For an example, visit [DuploCloud DevOps White Papers](https://duplocloud.com/white-papers/devops/#PAAS).

{% hint style="info" %}
DuploCloud provides flexibility when a feature not supported by DuploCloud can be programmed directly in your cloud provider. If you are using Terraform, then the DuploCloud provider and the native cloud provider can be used in tandem. For an example of this use case, see [https://duplocloud.com/white-papers/devops/#PAAS](https://duplocloud.com/white-papers/devops/#PAAS). Additionally, for specific needs such as creating short-lived one-shot ECS tasks, which are not directly supported through the Duplo UI or Terraform provider, DuploCloud offers the capability via its API. Customers have utilized this approach for tasks like database migrations on ECS, showcasing the platform's adaptability to unique operational requirements.
{% endhint %}

### I don't know IaC (Infrastructure-as-Code). Can I still use DuploCloud?

Yes. DuploCloud's UI is a No-Code DevOps interface. You do not need to know IaC or have cloud expertise to operate it. However, you should read the product documentation to understand the basic constructs. DuploCloud's approach significantly reduces the risk of errors associated with manual configurations or "Click Ops" and ensures that your infrastructure follows best practices with just a few clicks.

### Can we configure DuploCloud CLI on Windows Subsystem for Linux (WSL)?

Yes, but this process requires specific steps to ensure smooth operation, especially for tasks involving interactive browser sessions or AWS CLI usage. Users may need to install utilities like `xclip`, `xdg-utils`, and `jq` to facilitate these operations. Additionally, setting up aliases in the `.bashrc` file for `start` and `open` commands to point to `xdg-open`, and defining the `BROWSER` environment variable to the path of a browser in `/usr/local/bin` are crucial. Creating a symlink in `/usr/local/bin` to the browser executable in the Windows file system allows DuploCloud CLI to utilize the Windows browser for authentication and other browser-required operations. While optional, adding aliases for `pbcopy` and `pbpaste` can enhance script compatibility, particularly for users accustomed to macOS environments. These configurations enable effective use of DuploCloud CLI within WSL, bridging the gap between Windows and Linux environments for cloud management tasks.

### Are "No Code" and "Click Ops" the same?

No, these concepts are not the same. "Click Ops" is when engineers manually create infrastructure resources in the cloud and other UIs. This approach is often considered risky because the complexity of components and configurations makes it easy to make mistakes. DuploCloud's No-Code platform manages infrastructure resources for you, ensuring the underlying compute instances, firewall rules, IAM policies, and other components are configured following good practices. You only need a few clicks and don't need to know DevOps or SecOps because DuploCloud knows it for you.

Terraform projects typically have a broad scope with multiple components. Sometimes, you must make small targeted changes (for example, a health check URL change). But when the change is being executed, there may be other drifts, and the user may be forced to resolve them. This can be inconvenient, and often, the user will change the UI, resulting in further configuration drifts.

{% hint style="info" %}
About half of our customer base uses no-code, while the other half uses Terraform. Ironically, software developer-centric companies prefer no codeensure the application runs because it enables engineers to be agile and focus on their application code. By contrast, the low-code Terraform provider offers a different kind of flexibility, allowing for the integration of unique solutions like creating short-lived one-shot ECS tasks through the API, demonstrating the platform's versatility in accommodating diverse operational needs.
{% endhint %}

### Can you delete an application and all its resources with a single click and confirmation?

Yes, deleting a DuploCloud Tenant, which requires only a single click and confirmation, deletes the associated application and all its resources.&#x20;

### What can be automated using the DuploCloud API? How can API automation simplify application and resource management?

With DuploCloud, you can delete an application and all its associated resources with a single click (plus confirmation), streamlining the management process. Furthermore, every element in the DuploCloud UI can be automated over an API, ensuring that all resource provisioning is tracked and auditable.

### Does DuploCloud make any assumptions that may impact initial implementation time?

DuploCloud does not make any assumptions that could delay initial implementation. By segregating resources into environments called Tenants, DuploCloud accelerates ramp-up time.

## Connectivity and Availability FAQs

### How do I troubleshoot OpenVPN connection issues, such as DNS resolution failures?

OpenVPN connectivity issues (e.g., "hostname not found" errors when accessing resources like PostgreSQL DBs), especially on networks like T-Mobile 5G Home Internet, may be caused by DNS resolution failures. A workaround is to manually resolve the DNS name using a tool like MxToolbox and then use the IP address directly to bypass the DNS problem.

### How do I edit the Service Description to update my Control Plane configuration?

Once logging is enabled, the Service Description cannot be edited. To maintain the integrity and consistency of your logging setup, complete any Control Plane modifications before enabling central logging.&#x20;

### How do you create a Host with a public IP?

When creating a Host in the DuploCloud Portal, display **Advanced Options** and select the public subnet from the list of availability zones.

### How do I SSH into the Host?

Under each Host, you can click on **Connection Details** under the **Actions** list box, which will provide the key file and instructions to SSH.

### My host is Windows. How do I use Remote Desktop Protocol (RDP)?

When viewing a Host, click the **Actions** list box and select **Connection Details**. It will provide the password and instructions on how to connect to RDP.

### How do I get into the container where my code is running?

On the status page for the Service, find the Host where the container is running. SSH into the Host (see instructions above), and run `sudo docker ps` to get the container ID. Next, run `sudo docker exec -it`_**`CONTAINER_ID`**_`bash`. Find your container using the image ID.

### I cannot connect to my service URL. How do I debug it?

You can just run `ping` on your local machine to resolve the DNS name and make sure that the application is running `ping` from within the container. SSH into the Host and connect to your Docker container using the Docker command `sudo docker exec -t`_`CONTAINER_ID`_`bash`. From inside the container, curl the application URL using the IP `127.0.0.1` and the port where the application is running. Confirm that this works. CURL is the same URL using the container's IP address instead of `127.0.0.1`. The IP address can be obtained by running the `ifconfig` command in the container.

If the connection from within the container works, exit the container and navigate to the Host. Curl the same endpoint from the Host (i.e., using container IP and port). If this works, then under the ELB UI in DuploCloud, note down the Host port that DuploCloud created for the given container endpoint. This will be in the range of 10xxx or the same as the container port. Now try connecting to the `HostIP` and `DuploMappedHostPort` that was obtained. If this also works but the service URL fails, contact your enterprise admin or `duplolive-support@duplocloud.net`.

## Kubernetes FAQs

### Is Kubernetes required to use DuploCloud? Is using Kubernetes better than using ECS?

No, Kubernetes is not required to use DuploCloud. DuploCloud supports AWS (ECS and EKS), Kubernetes, Azure, and GCP. Many customers use software from multiple vendors to create robust business solutions backed by DuploCloud's compliance assurance and automated low-code/no-code DevOps approach.

The main advantage of Kubernetes is its broad-based, highly customizable, third-party, open-source community that supports it as a delivery platform. For example, Astronomer (managed Airflow), time series database, Istio service mesh, and Kong API Gateway all require a Kubernetes deployment. However, if your business needs and use cases are met with an AWS solution, you may not need Kubernetes. Choose the software that best aligns with your use cases and requirements.&#x20;

### I want to have multiple replicas of my Model-View-Controller (MVC) service. How do I make sure that only one of them runs migration?

Enable health check for your service, and ensure the API does not return `HTTP 200` status until migration. Since DuploCloud waits for a complete health check on one service before moving on to the next service, only one instance will run migration at a time.

DuploCloud's approach to container deployment emphasizes applications being self-contained and fungible, which facilitates independent updates of each service. Kubernetes automatically manages failing containers, and DuploCloud supports using Kubernetes health checks, including Liveness and Readiness Probes, to ensure containers function correctly and are ready to receive work.

## Storage FAQs

### Does DuploCloud Support custom S3 bucket naming?

DuploCloud supports the creation of S3 buckets with custom prefixes, enabling unique bucket names without the default numeric suffix. This feature can be activated by configuring a specific setting in the system, allowing for more personalized and easily identifiable bucket names that comply with Amazon S3's uniqueness requirements.

## Container/Docker FAQs

### One or more of my containers are pending. How can I debug them?

If the current status is Pending and the desired status is Running, wait a few minutes for the image to finish downloading. If it’s been more than five (5) minutes, check the faults from the button below the table. Ensure that your image name is correct and does not have spaces. Image names are case-sensitive, so they should be all lowercase, including image names in Docker Hub.

If the current state is Pending and the desired state is Delete, the container is the old service version. It is still running because the system is being upgraded, and the previous replica has not been upgraded yet. Check for faults for other containers in the same service with a current state of Pending and a desired state of Running.

### Some of my container statuses say `pending delete`. What does this mean?

This means DuploCloud is going to remove these containers. DuploCloud supports the creation of on-demand testing environments, facilitating quick setup and tear-down of environments with different configurations through the console or Terraform. This capability is crucial for testing and development workflows, ensuring flexibility and efficiency in managing containerized applications. An upgrade might be blocked if a Service's replica is upgraded, but not functioning correctly. To unblock the upgrade, restore the Service configuration (image, environment, etc.) to an error-free state.

## Terraform FAQs

### Is DuploCloud generating Terraform code behind the scenes to configure the cloud?

No. DuploCloud is calling the cloud provider's API directly. Based on user requirements, the software interacts with the cloud provider API asynchronously, maintaining a [state machine](https://en.wikipedia.org/wiki/Finite-state\_machine) of operations with built-in retries to ensure robustness. Interacting with the cloud provider continuously monitors configuration drift, system faults, security, and compliance controls.

### If DuploCloud is not generating Terraform code behind the scenes, how can I use Infrastructure-as-Code?

The Terraform and DuploCloud Web UIs layer on top of the DuploCloud platform.

![User Interaction with the DuploCloud Platform](<.gitbook/assets/image (11) (1) (1).png>)

DuploCloud provides Terraform with a Software Development Kit (SDK) called the [DuploCloud Terraform Provider](https://registry.terraform.io/providers/duplocloud/duplocloud/latest). This SDK allows users to configure their cloud infrastructure using DuploCloud constructs rather than lower-level cloud provider constructs. It enables users to benefit from Infrastructure-as-Code while significantly reducing the needed code. The DuploCloud Terraform Provider calls DuploCloud APIs. Our [DevOps white paper](https://duplocloud.com/white-papers/devops) provides detailed examples.

### **If my developers make changes via the DuploCloud UI, what happens to the Terraform code my DevOps engineers have written?**

It is best to create separation between your developers and your DevOps team. Using the DuploCloud UI to iterate product changes quickly in non-production development environments can create inconsistency.

Use Terraform to set up cloud services and handle the initial deployment of applications in both production and critical non-production environments. Additionally, create a CI/CD workflow that updates only the application deployment calls for Docker and Lambda. The DevOps team should manage any cloud service changes using Terraform, and developers should thoroughly understand these changes. However, developers should still be able to trigger CI/CD for their application rollouts independently, without DevOps involvement.

## Security and Compliance FAQs

### How can I set up Multi-Factor Authentication (MFA) for OpenVPN authentication?

From the DuploCloud Portal, click on your name in the top right corner and select **Profile**. Click on the VPN URL and enter the required credentials. On the first login, scan the barcode displayed on the screen. Download the Profile and add it to the OpenVPN Connect. Next time you log in with OpenVPN, you will be prompted to enter the authentication code.

### How much are SOC 2 Type 2 compliance costs?

Achieving SOC 2 Type 2 compliance is crucial for organizations looking to demonstrate high security and data protection. The process involves various costs, including using a Compliance Automation Platform, which may range from $10,000 to $15,000 or more for larger companies. The use of such platforms changes how the audit process is conducted. Understanding and managing these changes can cost between $7,500 and $15,000. Some companies offer both compliance tools and services. They may provide discounts if you bundle these services, offering a cost-saving opportunity. Companies starting their compliance journey should consult detailed resources to understand the expenses fully.

## CI/CD FAQs

### How does CI/CD work with DuploCloud?

CI/CD is the topmost layer of the DevOps stack. DuploCloud should be viewed as a deployment and monitoring solution invoked by your CI/CD pipelines, written with tools such as CircleCI, Jenkins, GitHub Actions, etc. You build images and push them to container registries without DuploCloud, but you invoke DuploCloud to update the container image. An example of this is in the [CI/CD documentation](introduction-to-ci-cd/). DuploCloud offers its [own CI/CD tool](introduction-to-ci-cd/katkit/) called KitKat.

### How do I uninstall Chocolatey?

Removing Chocolatey from your system is a straightforward process using PowerShell. Begin by executing `Remove-Item -Recurse -Force C:\ProgramData\chocolatey` to delete the Chocolatey directory and all its contents. Next, it's essential to clean up your system's PATH environment variable to eliminate any references to Chocolatey `bin` and `lib\bin` directories. This cleanup process ensures that Chocolatey and its components are thoroughly removed from your system, preventing potential conflicts or issues with other software installations or system operations. The DevOps team should do the same.

## Upgrade FAQs

### What is a rolling upgrade, and how do I enable it?

When you update (e.g., change an image or environment variable) a service with multiple replicas, DuploCloud changes one container at a time. If an updated container fails to start or the health check URL does not return `HTTP 200` status, DuploCloud will pause the upgrade of the remaining containers. If no health check URL is specified, DuploCloud only checks to see if an updated container is running before moving on to the next. To specify Health Check, use the Elastic Load Balancer menu to find the Health Check URL suffix.

## Diagnostic Tool FAQs

### How do I use Datadog and other diagnostics tools?

DuploCloud's out-of-the-box diagnostics stack is optional. To integrate with third-party toolset changes like Datadog, follow the guidelines and deploy collector agents as if running an application within the respective DuploCloud Tenant(s).

## Error Messages

### I'm receiving the error message: `Could not load credentials from any providers`.

Your `duplo-jit` local cache must be cleared. To do this, run the following command: `rm -rf ~/Library/Caches/duplo-jit/`

### When creating a Service, I'm receiving the message: `DuploCloud Fault Conditions Unschedulable` because 0/N nodes are available: one node(s) didn't match pod anti-affinity rules, and one node(s) was unschedulable.

Two possible reasons for receiving this message are:

* You are not allocating enough Hosts to process your workload.
* The [allocation tags](overview-1/container-deployments/concepts.md#allocation-tags) you assigned to your existing Hosts limit additional Service workloads.

### I do not see logs displayed for a Tenant. I get the error: `Docker native collection agent Filebeat is not running for Tenant`.

Ensure logging is set up and the correct Tenant is selected. If logs are still not appearing in the DuploCloud console and Filebeat indicates a bulk send failure, Elasticsearch may be out of disk space. In this case, check the disk space in the Default Tenant diagnostics history. If necessary, follow the steps to recognize and expand the volume on Linux as outlined in the AWS documentation to resolve this issue.

### I'm receiving the message: `It took too long to check if you are authorized to access DuploCloud. Try refreshing the page and logging in again`.

Clear your browser cache or use a private browsing window. If the problem persists, request assistance from DuploCloud to ensure a smooth login experience.
