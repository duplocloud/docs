---
description: Popular and frequently asked questions about DuploCloud and AWS
---

# AWS FAQ

## General FAQs

### AWS Copilot seems to be a low-code, developer-friendly tool that uses existing AWS tools for monitoring. Can AWS Copilot be used with/instead of DuploCloud?

AWS Copilot is used only for ECS cluster management, which is just a small subset of overall Cloud operations. In the chart below, you can see that DuploCloud includes container management in addition to multiple other functions. You can still use Copilot with DuploCloud for ECS management. Other clients have used tools like Harness or Helm with DuploCloud for Kubernetes management.

<div align="left">

<figure><img src="../.gitbook/assets/DC_Capabilities.png" alt=""><figcaption><p>DuploCloud features</p></figcaption></figure>

</div>

### What keys should I use in my application to connect to the AWS resources I have created in DuploCloud (S3, Dynamo, SQS)? <a href="#id-4-toc-title" id="id-4-toc-title"></a>

If your application is running in a DuploCloud [Tenant](../getting-started/application-focussed-interface/tenant/) you do not need a long-term credential, such as an AWS access key. After your application is running in the Tenant, test your connection using the AWS CLI to verify access.   &#x20;

Use the AWS constructor that takes only the region as the argument (`us-west-2`). DuploCloud setup links your instance profile and the resources. The host in DuploCloud already has access to the resources within the same tenant\project. DuploCloud AWS resources are reachable only from DuploCloud Hosts on the same account.

{% hint style="info" %}
**IMPORTANT:** You cannot connect to any DuploCloud AWS resource from your local machine.
{% endhint %}

## Does Duplo use an AWS instance profile or access keys to access  AWS accounts?

Duplo uses an IAM role, specifically an instance profile, for accessing AWS accounts. There are no access keys involved in this methodology.

## Security and Compliance FAQs

### With DuploCloud, will we be more secure and compliant out-of-the-box, as opposed to using a default AWS configuration?

Yes. This is a major advantage of using DuploCloud. All controls are mapped to various compliance standards. DuploCloud is also very flexible in enabling you to add custom policies (resource quotas, ability to create public-facing endpoints, etc.).

## CI/CD FAQs

### Do I need an AWS access key for my application when using AWS?

CI/CD is the topmost layer of the DevOps stack. DuploCloud should be viewed as a deployment and monitoring solution that is invoked by your CI/CD pipelines, written with tools such as CircleCI, Jenkins, GitHub Actions, etc. You build images and push them to container registries without involving DuploCloud, but invoke DuploCloud to update the container image. An example of this is in the [CI/CD](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/\~/changes/r966TcV3ISnUcfuJxUa3/ci-cd/continuous-integration-and-deployment-ci-cd) section. DuploCloud offers its own CI/CD tool ([KatKit](../ci-cd/katkit/)), as well.

If your application is running in a DuploCloud [Tenant](../getting-started/application-focussed-interface/tenant/) you do not need a long-term credential, such as an AWS access key. After your application is running in the Tenant, test your connection using the AWS CLI to verify access. For more information, see the [AWS FAQ](aws-faq.md).  &#x20;

## Kubernetes FAQs

### How do I look at detailed Load Balancer settings for my K8s Service?

DuploCloud provisions a Load Balancer for your K8 service. If you want to look at detailed settings on the Load Balancer like Idle timeout, Access logs, and others, you can find and view them directly in AWS, by following the below steps:

You can find the Load Balancer name for your service by navigating to **Kubernetes** _->_ **Services**, selecting your Service from the list, and looking at the Load Balancer tab. If you're using K8s Ingress then you will have to go to the K8s Ingress tab and find the Load Balancer configuration there.

Once you have the Load Balancer name, you can go to the AWS Console via the DuploCloud UI ([here](use-cases/jit-access.md)). Once you are in the AWS Console, navigate to the EC2 service view and navigate to Load Balancers from the left navigation menu. Find your Load Balancer by name from that list and look at the detailed attributes in that view (scroll down to attributes).

## Terraform FAQs

### Why use Terraform when Cloud Formation is AWS native?

Many customers prefer Terraform to CloudFormation. Many elements in the Cloud DevOps cycle can be non-AWS (such as native Kubernetes, MongoDB, Data Dog, Okta, etc.), and all support Terraform providers.

## Performance FAQs

### Is the Duplocloud instance a single point of failure, and if so, to what extent? Who manages this instance?

No. DuploCloud achieves High Availability (HA) using cluster management. And because you own your AWS account, your data is always secure in AWS.&#x20;

Our customers have never been blocked from performing urgent configuration updates because DuploCloud is unavailable. If DuploCloud is down, it is similar to your DevOps engineer being unavailable. In this case, someone else can take their place by directly configuring AWS.&#x20;

Our customers consider this single-platform approach very beneficial for both centralizing operations and maximizing developer access. DuploCloud runs in a VM in your account. We manage this VM with your permission, and we can also give you simple steps to troubleshoot or install new updates. We are available 24x7 and work as your extended DevOps team.

### Is scaling handled differently from ECS, where you set thresholds and min/max instances to spin up/down?

No. DuploCloud manages scale in the same way. We expose these thresholds in a simple form that is much easier to configure, even for a user with no DevOps experience. Behind the scenes, DuploCloud maps to the same native AWS constructs.

## Relational Database Service (RDS) FAQS&#x20;

### Is attaching an RDS instance to each application for spin-up/down purposes expensive? Some of our RDS instances are small.

Small instances are generally no problem. DuploCloud can manage dynamic database spin-up/down with a single RDS database. Sharing AWS services in dynamic environments also helps reduce costs.

### Can an RDS be left intact if I only want to destroy the application and not the database?

Yes.

### Can I upgrade RDS versions?

Yes. Use [AWS Console](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER\_UpgradeDBInstance.Upgrading.html) and see your Cloud Provider for compatibility requirements. Note that while versions 5.7.40, 5.7.41, and 5.7.42 cannot be upgraded to version 8.0.28, you can upgrade these versions to version 8.0.32 and higher.&#x20;

### Our current RDS logs are sent to CloudWatch. Does DuploCloud support this?&#x20;

Yes.

## EKS Version Upgrade FAQs

### What is the process for EKS upgrades and how does DuploCloud support them?

DuploCloud creates and tests changes to the DuploCloud platform to support the new EKS version. Once testing is complete, updates are rolled out on the DuploCloud customer platform. Then, users can update the EKS version.

### **How do EKS and DuploCloud version upgrades align?**&#x20;

There may be a delay between the release of a new EKS version and a DuploCloud version that supports it. This is due to the time needed to develop and test changes to the DuploCloud platform. DuploCloud ensures customers are on a supported/non-deprecated version of EKS at all times.

### **How will we be notified when we are ready for an EKS upgrade?**

DuploCloud notifies users when an EKS upgrade is planned.

### **What is the upgrade plan scope?**&#x20;

The upgrade plan scope includes everything (by DuploCloud or Helm) deployed on the cluster.



