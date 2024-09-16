---
description: An outline of the DuploCloud approach compared to existing DevOps
cover: ../.gitbook/assets/Linkedin-bannerV3 (1).png
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

## **Existing Approach**

Technology organizations today typically have people with two distinct skill sets: Software Engineers and DevOps Engineers. Compliance functions may be managed by these engineers or by a separate team. In startups and smaller companies, engineers may wear all three hats.

Software Engineers design high-level application architectures that typically include multiple environments (Dev, Stage, QA, Production, etc.), CI/CD pipelines, and diagnostics like central logging, monitoring, and alerting. The business dictates specific compliance standards like PCI, HIPAA, SOC 2, etc. All this information is passed to the DevOps team, who translates it into cloud infrastructure configurations.

<figure><img src="../.gitbook/assets/app reqs.png" alt=""><figcaption><p>A diagram of typical application engineering requirements</p></figcaption></figure>

DevOps Engineers must manually convert requirements into hundreds or thousands of lower-level configurations, best practices, and compliance controls such as IAM Roles, Instance profiles, KMS Keys, PEM keys, vulnerability scanning systems, virus scanners, VPC, Security Groups, Intrusion detection, etc. This translation is usually done based on human knowledge and subject matter expertise and often requires thousands of lines of code using languages like Terraform, Python, and Bash.

A common misconception is that tools like Terraform fully automate DevOps workflows. Terraform is only a programming language. One needs substantial infrastructure know-how to build automation using Terraform. DevOps engineers often lack awareness of compliance nuances beyond best practices and must revisit and redo their work frequently to ensure compliance.

DevOps essentially requires one to be a programmer, an operator, and a compliance expert: three distinct skill sets that have never traditionally co-existed in the IT industry. This is the primary challenge in the DevOps space.

## **DuploCloud Approach**

DuploCloud simplifies and automates cloud infrastructure management by enabling users to deploy and operate applications without knowledge of lower-level DevOps nuances. The platform requires only three high-level inputs:

1\.     Application architecture

2\.     Compliance standards (SOC 2, PCI, HIPAA, etc.)

3\.     Public cloud provider

With these inputs, DuploCloud generates all the lower-level configurations to adhere to DevOps best practices and required compliance standards.

DuploCloud's core approach to security and compliance is out-of-box compliance so users don't have to learn and apply compliance controls. DuploCloud supports PCI, HIPAA, SOC 2, HITRUST, NIST, ISO, GDPR, and more. See the [DuploCloud documentation](../security-and-compliance/) to learn more about how DuploCloud provides unparalleled security and compliance.

Users interact with their applications through the No-Code DuploCloud UI or our Low-Code Terraform provider, operating directly on cloud constructs like S3 buckets, DynamoDB, Lambda functions, and more, without sacrificing flexibility or scalability. The DuploCloud Terraform provider enables users to achieve the same automation with a tenth of the code and significantly fewer DevOps skills than native Terraform.

{% hint style="info" %}
A common misconception is that DuploCloud generates Terraform behind the scenes to provision the cloud infrastructure. The DuploCloud UI and Terraform (with the DuploCloud Provider) are layered on top of DuploCloud. Behind the scenes, DuploCloud uses the cloud provider Application Programming Interfaces (APIs) as shown in the picture below.
{% endhint %}

![](<../.gitbook/assets/image (4) (1) (1).png>)

Unlike a PAAS such as Heroku, the DuploCloud platform does not prevent users from consuming cloud services directly from the cloud provider. DuploCloud is a self-hosted platform running in the customer's cloud account and can therefore work in tandem with direct cloud account changes. Complex security details (IAM roles, KMS keys, Azure Managed Identities, GCP service accounts, etc.) are hidden, but remain configurable if needed. See this [DuploCloud white paper](https://duplocloud.com/white-papers/devops/) for more information and examples.

DuploCloud uses APIs to handle tasks in the background (e.g., processing user requests, generating configurations synchronously, and calling the cloud provider). Other operations require asynchronous processing, requiring a state machine with retries that continuously identifies and corrects configuration drift and continuously monitors faults and compliance controls.

DuploCloud eliminates the need for extensive manual coding and drastically reduces the need for specialized DevOps expertise. At the same time, the platform ensures efficient, scalable, and compliant cloud infrastructure deployment and management, making it a superior alternative to traditional methods.

![A visual representation of the work done by DuploCloud](<../.gitbook/assets/Screen Shot 2022-03-12 at 1.34.37 PM.png>)

