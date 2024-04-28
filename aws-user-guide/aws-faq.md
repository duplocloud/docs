---
description: Popular and frequently asked questions about DuploCloud and AWS
---

# AWS FAQ

## General FAQs

### What is AWS?

AWS, or Amazon Web Services, is a comprehensive cloud computing platform provided by Amazon. It offers a broad array of services including computing power, storage options, and networking capabilities, enabling businesses to scale and grow by leveraging cloud technology without the need for physical hardware.

### AWS Copilot seems to be a low-code, developer-friendly tool that uses existing AWS tools for monitoring. Can AWS Copilot be used with/instead of DuploCloud?

AWS Copilot is specifically designed for ECS cluster management, representing just a fraction of the broader cloud operations landscape. DuploCloud encompasses container management among a suite of other functionalities, allowing for the use of Copilot for ECS management within its ecosystem. Additionally, DuploCloud users have integrated other tools like Harness or Helm for Kubernetes management, showcasing the platform's versatility.

<div align="left">

<figure><img src="../.gitbook/assets/DC_Capabilities.png" alt=""><figcaption><p>DuploCloud features</p></figcaption></figure>

</div>

### What keys should I use in my application to connect to the AWS resources I have created in DuploCloud (S3, Dynamo, SQS)? <a href="#id-4-toc-title" id="id-4-toc-title"></a>

For applications running within a DuploCloud Tenant, long-term credentials like AWS access keys are unnecessary. DuploCloud automates the linkage between your instance profile and AWS resources, ensuring secure access. It's important to note that DuploCloud AWS resources are accessible exclusively from DuploCloud Hosts within the same account, prohibiting direct connections from local machines.

{% hint style="info" %}
**IMPORTANT:** Direct connection to DuploCloud AWS resources from local machines is not supported.
{% endhint %}

## Security and Compliance FAQs

### With DuploCloud, will we be more secure and compliant out-of-the-box, as opposed to using a default AWS configuration?

DuploCloud significantly enhances security and compliance by default, offering a comprehensive mapping of controls to various standards. It also provides the flexibility to implement custom policies, ensuring a tailored security posture that meets specific organizational needs.

## CI/CD FAQs

### Do I need an AWS access key for my application when using AWS?

In the context of CI/CD, DuploCloud serves as a deployment and monitoring solution that integrates seamlessly with your CI/CD pipelines. This eliminates the need for AWS access keys for applications running within a DuploCloud Tenant, streamlining the deployment process. DuploCloud's integration capabilities are further highlighted in its own CI/CD tool, KatKit, and its compatibility with popular tools like CircleCI, Jenkins, and GitHub Actions.

## Kubernetes FAQs

### How do I look at detailed Load Balancer settings for my K8s Service?

DuploCloud simplifies the management of Load Balancers for Kubernetes services, providing a direct pathway to detailed settings such as Idle timeout and Access logs. This is achieved through the DuploCloud UI, which facilitates access to the AWS Console for in-depth configuration and monitoring.

## Terraform FAQs

### Why use Terraform when Cloud Formation is AWS native?

Terraform's broad compatibility with both AWS and non-AWS services, including Kubernetes, MongoDB, and Data Dog, makes it a preferred choice for many organizations. This flexibility supports a diverse and integrated DevOps ecosystem beyond the AWS-native CloudFormation.

## Performance FAQs

### Is the Duplocloud instance a single point of failure, and if so, to what extent? Who manages this instance?

DuploCloud's architecture ensures High Availability (HA) through effective cluster management, mitigating the risk of a single point of failure. The platform operates within your AWS account, with DuploCloud providing 24x7 support and management, ensuring both operational continuity and security of your data.

### Is scaling handled differently from ECS, where you set thresholds and min/max instances to spin up/down?

Scaling within DuploCloud mirrors the native AWS approach, offering an intuitive interface for configuring thresholds and scaling policies. This simplifies the scaling process, making it accessible even to users with limited DevOps expertise, while still leveraging AWS's robust scaling capabilities.

## Relational Database Service (RDS) FAQS

### Is attaching an RDS instance to each application for spin-up/down purposes expensive? Some of our RDS instances are small.

DuploCloud efficiently manages RDS instances, accommodating dynamic database requirements without significant cost implications, even for smaller instances. This approach facilitates cost-effective sharing of AWS services across dynamic environments.

### Can an RDS be left intact if I only want to destroy the application and not the database?

Yes, DuploCloud allows for the selective retention of RDS instances independent of application lifecycle, providing flexibility in resource management.

### Can I upgrade RDS versions?

Upgrading RDS versions is supported through the AWS Console, with DuploCloud facilitating easy access to this functionality. It's important to consult AWS documentation for specific version compatibility and upgrade paths.

### Our current RDS logs are sent to CloudWatch. Does DuploCloud support this?

Yes, DuploCloud supports the integration of RDS logs with CloudWatch, ensuring comprehensive monitoring and logging capabilities.