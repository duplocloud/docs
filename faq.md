---
description: Popular and frequently asked questions
---

# FAQ

{% hint style="info" %}
**NOTICE:** This document provides frequently asked questions related to the high level architecture and business model. For more detailed technical FAQ please refer to the [AWS FAQ](aws/aws-faq.md) or [Azure FAQ](https://docs.duplocloud.com/docs/v/azure/faq)
{% endhint %}

### Is DuploCloud a SaaS product?

No. DuploCloud is a self-hosted solution that is deployed within the customer's cloud account. This hosted solution provides the customer with a SaaS-like experience. If the customer desires, DuploCloud also provides a fully managed service to maintain uptime, provide updates and on-going support.

### What cloud providers are supported?

DuploCloud supports the following public cloud providers:

* Amazon AWS
* Microsoft Azure
* Google Cloud

### Can I use DuploCloud if I don't have any DevOps expertise in my company?

Absolutely! In fact, more than half of our customers have no DevOps team. The DuploCloud team will act as your extended DevOps team that assists with white glove onboarding setup, as well as daily operations. We cover what is supported in the DuploCloud platform as well as assisting with other issues for your cloud provider. We are available 24x7 via Slack. However, we request that after the initial onboarding of the platform, you engage the DuploCloud team as the second line of defense for any issues by setting up an initial triage process of your own. We can assist with this process.

### What level of Support does the DuploCloud team provide?

The DuploCloud team will act as your extended DevOps team starting with white glove onboarding, setup, and assisting with daily operations. We cover what is supported in the DuploCloud platform as well as assisting with other issues for your cloud provider. We are available 24x7 via Slack. However, we request that after the initial onboarding of the platform, you engage the DuploCloud team as the second line of defense for any issues by setting up an initial triage process of your own. We can assist with this process. Most likely you will find a resolution in the platform and if not, simply ping the DuploCloud team.

In our managed service offering we will also do your deployments, be the first line of defense for any issues and are constantly involved in daily tasks like CI/CD updates, etc.

{% hint style="info" %}
DuploCloud is like your extended DevOps team available 24x7 on your slack channel, phone and email.
{% endhint %}

### Can I make changes directly in the cloud account managed by DuploCloud?

Yes. In fact many times this is required because DuploCloud may not support all cloud features or configurations. Direct changes to your cloud can be categorized in 3 groups:

\
\- **Independent Changes.** DuploCloud labels the resources and configurations it manages. If completely independent changes are being made directly at the cloud provider, DuploCloud will not interfere. However, DuploCloud still monitors the changes from a compliance perspective and alerts for any non-compliant configurations.

\
\- **Non-conflicting changes to DuploCloud managed resources**. An example of this could be adding forwarding rules to a load balancer created through DuploCloud. In this case this is a configuration that DuploCloud is not directly managing and there is no problem with making the change directly at the cloud provider.

\
\- **Conflicting Changes to DuploCloud managed resources.** In such a case DuploCloud will detect the conflicts and will either revert the change or raise an alert about the inconsistency.

{% hint style="info" %}
DuploCloud provides full flexibility where a certain feature that is not supported in the platform can programmed directly in the cloud provider. If one is using Terraform, then the DuploCloud Provider as well as the native cloud provider can be used in tandem. An example is shown here [https://duplocloud.com/white-papers/devops/#PAAS](https://duplocloud.com/white-papers/devops/#PAAS)
{% endhint %}

### **Is DuploCloud generating Terraform code behind the scenes to configure the cloud?**

No. DuploCloud is calling your cloud provider API directly. Based on the user requirements, the software interacts with the cloud provider API asynchronously, maintaining a state machine of operations, with retries built-in to ensure robustness. Any configuration drift, system faults, security and compliance controls are monitored continuously by interacting with the cloud provider.

### If DuploCloud is not generating Terraform code behind the scenes, then how can I use Infrastructure-as-code?

Terraform and DuploCloud Web UI are both layers on top of the DuploCloud platform.

![User Interaction with the DuploCloud Platform](<.gitbook/assets/image (10).png>)

DuploCloud provides an SDK into Terraform called the [DuploCloud Terraform Provider](https://registry.terraform.io/providers/duplocloud/duplocloud/latest). This SDK allows the user to configure the cloud infrastructure using DuploCloud constructs, rather than directly using lower level cloud provider constructs. This allows the user to get the benefits of Infrastructure-as-Code while significantly reducing the amount of code that needs to be written. The DuploCloud Terraform Provider simply calls DuploCloud APIs. This white-paper provides detailed examples: [https://duplocloud.com/white-papers/devops](https://duplocloud.com/white-papers/devops/#PAAS)

### **Am I locked in to DuploCloud? If I wanted to move away from DuploCloud, what work do I need to do?**

DuploCloud is running in your own cloud account where all your workloads are hosted as well. DuploCloud is a provisioning system. Stopping DuploCloud does not impact any of your applications and cloud services.

The following is a list of automation constructs managed by DuploCloud, and a summary of what a user needs to do in order to maintain them directly instead of DuploCloud.

1. Cloud Provider Configuration (Terraform): This involves various cloud services, IAM roles, Security groups, VPC, etc. DuploCloud can export your latest cloud configuration into native Terraform code and state files. Once exported, you can maintain them directly going forward.
2. Kubernetes: All applications and configurations that have been deployed in K8S are available as is in the form of deployments, statefulset, daemonset, K8S Secrets, config maps, etc. One can run simple _kubectl_ commands to export those configurations as _yaml_ files and continue to maintain them going forward.
3. Compliance monitoring: DuploCloud uses a third party SIEM solution called [Wazuh](https://www.wazuh.com). This is an open source software platform running in an independent VM in your cloud account and you have full permissions to retain it as-is. However, going forward any new systems that need compliance monitoring need to be wired into the SIEM by you.
4. Diagnostics tools: These include Prometheus, Grafana and Elasticsearch. All of these are open source and run in your cloud account. You can continue to manage them directly.

{% hint style="info" %}
If DuploCloud is down, its like your DevOps engineer not being reachable and if DuploCloud needs to be opted-out it's like letting go of the current DevOps team and having the new one take over. DuploCloud is neither a PAAS nor a hosted solution where your workloads are being hosted.
{% endhint %}

### **I don't know IaC (Infrastructure-as-Code), can I still use DuploCloud?**

Yes. DuploCloud's Web UI is a no-code interface for DevOps. You do not need to know IaC or require any cloud expertise in order to operate it. You simply need to understand the basic constructs in DuploCloud by reading the product documentation.

### My application developers **don't know IaC (Infrastructure-as-Code), but my DevOps engineers do. If my developers make changes via the DuploCloud UI what happens to the Terraform code my DevOps engineers have written?**

This will cause an inconsistency, so you will have create some separation between your developers and your DevOps team. One example is allowing developers to use the Web UI in non-production(dev) environments in order to quickly iterate product changes. Production and critical non-production environments, the cloud services setup, as well as first time application deployment can be done via Terraform code. CI/CD workflows can be built which only update the application (Docker and Lambda) deployments. Any cloud service level change should be done by the DevOps team via Terraform and the developers will have to ask the DevOps team for the same. Developers should still be able to trigger CI/CD for their application rollouts without DevOps involvement.

### **From the DuploCloud team's experience what is good for me, Low-code or No-code?**

The answer depends on two key factors:

\
1\. **How much Developer self-service is required, and are you an operations-centric organization**? In cases, especially in a fast growing company environment, where architecture is constantly evolving and services are being constantly updated, there may be a desire to let developers self-service and move fast. This would be a case for no-code. On the other hand, in cases where there is an operations organization and everything is required to be centralized, then the low-code Terraform solution may be a better option.\
Note that Terraform is a client side scripting tool and hence it is a single user system, meaning within the scope of a project only one person can be making changes. One may feel constrained if a project has many components and two people cannot operate even if they are dealing with completely independent constructs.\
\
2\. **Dealing with broad scope of changes vs. small just-in-time changes**. Terraform projects typically will have a broad coverage with multiple components. At times one needs to make a small targeted change (say a health check url change) but when the change is being executed there may be other "drifts" and the user will be forced to resolve them. This can be very inconvenient and more often than not the user will make the change in the UI. This will end up further drifting the Terraform state for future updates.

{% hint style="info" %}
About half of our customer base uses no-code while other half uses Terraform. Ironically software developer centric companies prefer no-code because engineers are able to move fast and stay focussed on their own application code. In DevOps centric organizations people use our low-code Terraform provider.
{% endhint %}

### How do I use my own diagnostics tools like Datadog?

DuploCloud's out-of-the-box diagnostics stack is optional. To integrate with your own toolset like Datadog you would follow their guidelines which typically would be to deploy some collector agents. You can do that like a regular application within the respective tenants.

### How will CI/CD work with DuploCloud?

CI/CD is the top most layer of the DevOps stack. DuploCloud should be looked at as a deployment and monitoring solution which can be invoked by your CI/CD pipelines written in tools like CircleCI, Jenkins, GitHub Actions, etc. Basically, one would build the images and push to container registries without involving DuploCloud, but invoke DuploCloud to update the container image. An example of this is in the CI/CD section. DuploCloud does offer its own CI/CD tool as well.
