---
description: An overview of the DuploCloud Portal
cover: ../.gitbook/assets/GitHub - Great Place to Work Badge.png
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

# Getting Started with DuploCloud

This module describes DuploCloud and its unique constructs and terminology. It also outlines the onboarding process and details the business value of automating your DevOps and Security Compliance cloud environments in the DuploCloud Portal.

## **Existing Approach**

Technology organizations today typically have people with two distinct skill sets: Software Engineers and DevOps Engineers. Compliance functions may be managed by these engineers or by a separate team. In startups and smaller companies, engineers may wear all three hats.

Software Engineers design high-level application architectures that typically include multiple environments (Dev, Stage, QA, Production, etc.), CI/CD pipelines, and diagnostics like central logging, monitoring, and alerting. The business dictates specific compliance standards like PCI, HIPAA, SOC 2, etc. All this information is passed to the DevOps team, who translates it into cloud infrastructure configurations.

<figure><img src="../.gitbook/assets/app reqs.png" alt=""><figcaption><p>A diagram of typical application engineering requirements</p></figcaption></figure>

DevOps Engineers must manually convert requirements into hundreds or thousands of lower-level configurations, best practices, and compliance controls such as IAM Roles, Instance profiles, KMS Keys, PEM keys, vulnerability scanning systems, virus scanners, VPC, Security Groups, Intrusion detection, etc. This translation is usually done based on human knowledge and subject matter expertise and often requires thousands of lines of code using languages like Terraform, Python, and Bash.

A common misconception is that tools like Terraform fully automate DevOps workflows. Terraform is only a programming language. One needs substantial infrastructure know-how to build automation using Terraform. DevOps engineers often lack awareness of compliance nuances beyond best practices and must revisit and redo their work frequently to ensure compliance.

DevOps essentially requires one to be a programmer, an operator, and a compliance expert: three distinct skill sets that have never traditionally co-existed in the IT industry. This is the primary challenge in the DevOps space.

## **DuploCloud Approach**

&#x20;DuploCloud simplifies and automates cloud infrastructure management by enabling users to deploy and operate applications without knowledge of lower-level DevOps nuances. The platform requires only three high-level inputs:

1\.     Application architecture

2\.     Compliance standards (SOC 2, PCI, HIPAA, etc.)

3\.     Public cloud provider

With these inputs, DuploCloud generates all the lower-level configurations necessary to adhere to DevOps best practices and required compliance standards.

DuploCloud's core approach to security and compliance is out-of-box compliance so users don't have to learn and apply compliance controls. DuploCloud supports PCI, HIPAA, SOC 2, HITRUST, NIST, ISO, GDPR, and more. See the [DuploCloud documentation](../security-and-compliance/) to learn more about how DuploCloud provides unparalleled security and compliance.

Users interact with their applications through the no-code DuploCloud UI or a low-code Terraform provider, operating directly on cloud constructs like S3, DynamoDB, Lambda functions, and more, without sacrificing flexibility or scalability. The DuploCloud Terraform provider enables users to achieve the same automation with 10x less code and significantly fewer DevOps skills than native Terraform.

Unlike a PAAS such as Heroku, the DuploCloud platform does not prevent users from consuming cloud services directly from the cloud provider. DuploCloud is a self-hosted platform running in the customer's cloud account and can therefore work in tandem with direct cloud account changes. Complex security details (IAM roles, KMS keys, Azure Managed Identities, GCP service accounts, etc.) are hidden, but remain configurable if needed. See this [DuploCloud white paper](https://duplocloud.com/white-papers/devops/) for more information and examples.

![A visual representation of the work done by DuploCloud](<../.gitbook/assets/Screen Shot 2022-03-12 at 1.34.37 PM.png>)

DuploCloud eliminates the need for extensive manual coding and drastically reduces the need for specialized DevOps expertise. At the same time, the platform ensures efficient, scalable, and compliant cloud infrastructure deployment and management, making it a superior alternative to traditional methods.

## No-Code/Low-Code

DuploCloud provides a no-code UI-based approach to building and operating cloud infrastructures.&#x20;

For users who want to use Infrastructure-as-Code (IaC), we have a [Terraform](https://registry.terraform.io/providers/duplocloud/duplocloud/latest) provider that enables low-code IaC. This provider exposes all DuploCloud abstractions and constructs to be programmed using Terraform. This allows users with no DevOps or SecOps expertise to build infrastructure, with all compliance controls built in, using one-tenth of the code required by native Terraform. This [whitepaper ](https://duplocloud.com/white-papers/devops/)describes the process in detail.

{% hint style="info" %}
A common misconception is that DuploCloud generates Terraform behind the scenes to provision the cloud infrastructure. The DuploCloud UI and Terraform (with the DuploCloud Provider) are layered on top of DuploCloud. Behind the scenes, DuploCloud uses the cloud provider Application Programming Interfaces (APIs) as shown in the picture below.
{% endhint %}

![](<../.gitbook/assets/image (4) (1) (1).png>)

DuploCloud uses APIs to handle tasks in the background (e.g., processing user requests, generating configurations synchronously, and calling the cloud provider). Other operations require asynchronous processing, requiring a state machine with retries that continuously identifies and corrects configuration drift. Faults and compliance controls must be monitored continuously.

Scripting tools like Terraform are meant to be run with human supervision. Scripts run sequentially without parallel processing or retry capabilities.

Visit our [Video Library](https://www.duplocloud.com/videos/) for demos. For more information about No-Code/Low-Code and how it relates to Click Ops, [see this FAQ](../faq.md#isnt-no-code-just-click-ops-everyone-says-i-shouldnt-do-that).&#x20;
