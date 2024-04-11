---
description: Popular and frequently asked questions about DuploCloud and AWS
---

# AWS FAQ

## With DuploCloud, will we be more secure and compliant out-of-the-box, as opposed to using a default AWS configuration?

Yes. This is a major advantage of using DuploCloud. All controls are mapped to various compliance standards. DuploCloud is also very flexible in enabling you to add custom policies (resource quotas, ability to create public-facing endpoints, etc.)

## Do I need an AWS access key for my application when using AWS?

CI/CD is the topmost layer of the DevOps stack. DuploCloud should be viewed as a deployment and monitoring solution that is invoked by your CI/CD pipelines, written with tools such as CircleCI, Jenkins, GitHub Actions, etc. You build images and push them to container registries without involving DuploCloud, but invoke DuploCloud to update the container image. An example of this is in the [CI/CD](https://app.gitbook.com/o/ojpRPRrP7bqrzOUuLmOz/s/68cb0s9ce5UIUKWPuYs8/\~/changes/r966TcV3ISnUcfuJxUa3/ci-cd/continuous-integration-and-deployment-ci-cd) section. DuploCloud offers its own CI/CD tool ([KatKit](../ci-cd/katkit/)), as well.

If your application is running in a DuploCloud [Tenant](../getting-started-1/application-focussed-interface/tenant/) you do not need a long-term credential, such as an AWS access key. After your application is running in the Tenant, test your connection using the AWS CLI to verify access. For more information, see the [AWS FAQ](aws-faq.md).  &#x20;

## What keys should I use in my application to connect to the AWS resources I have created in DuploCloud (S3, Dynamo, SQS)? <a href="#id-4-toc-title" id="id-4-toc-title"></a>

If your application is running in a DuploCloud [Tenant](../getting-started-1/application-focussed-interface/tenant/) you do not need a long-term credential, such as an AWS access key. After your application is running in the Tenant, test your connection using the AWS CLI to verify access.   &#x20;

Use the AWS constructor that takes only the region as the argument (`us-west-2`). DuploCloud setup links your instance profile and the resources. The host in DuploCloud already has access to the resources within the same tenant\project. DuploCloud AWS resources are reachable only from DuploCloud Hosts on the same account.

{% hint style="info" %}
**IMPORTANT:** You cannot connect to any DuploCloud AWS resource from your local machine.
{% endhint %}

## How do I look at detailed load balancer settings for my K8s Service?

DuploCloud provisions a load balancer for your K8 service. If you want to look at detailed settings on the load balancer like Idle timeout, Access logs, and others, you can find and view them directly in AWS, by following the below steps:

You can find the load balancer name for your service by navigating to **Kubernetes** _->_  **Services**, selecting your Service from the list, and looking at the Load Balancer tab. If you're using K8s Ingress then you will have to go to the K8s Ingress tab and find the Load Balancer configuration there.

Once you have the load balancer name, you can go to the AWS console via the DuploCloud UI ([here](use-cases/jit-access.md)). Once you are in the AWS Console, navigate to the EC2 service view and navigate to Load Balancers from the left navigation menu. Find your load balancer by name from that list and look at the detailed attributes in that view (scroll down to attributes)

## Why use Terraform when Cloud Formation is AWS native?

Many customers prefer Terraform to CloudFormation. Many elements in the Cloud DevOps cycle can be non-AWS (such as native Kubernetes, MongoDB, Data Dog, Okta, etc.), and all support Terraform providers.

## AWS Copilot seems to be a low-code tool and developer-friendly. I understand that Copilot relies on existing AWS tools to monitor.

AWS Copilot is used only for ECS cluster management, which is just a small subset of overall Cloud operations. In the chart below, you can see that DuploCloud includes container management in addition to multiple other functions. You can still use Copilot with DuploCloud for ECS management. Other clients have used tools like Harness or using Helm with DuploCloud for Kubernetes management.

<figure><img src="../.gitbook/assets/DC_Capabilities.png" alt=""><figcaption><p>DuploCloud features</p></figcaption></figure>

## Is the Duplocloud instance a single point of failure, and to what extent, if so? Who manages this instance?

No. DuploCloud achieves High Availability (HA) using cluster management. And because you own your AWS account, your data is always secure in AWS.&#x20;

Our customers have never been blocked from performing urgent configuration updates because DuploCloud is unavailable. If DuploCloud is down, it is similar to your DevOps engineer being unavailable. In this case, someone else can take their place by directly configuring AWS.&#x20;

Our customers consider this single-platform approach very beneficial for both centralizing operations and maximizing developer access. DuploCloud runs in a VM in your account. We manage this VM with your permission, and we can also give you simple steps to troubleshoot or install new updates. We are available 24x7 and work as your extended DevOps team.

## With DuploCloud, will we be more secure and compliant out-of-the-box, as opposed to using a default AWS configuration?

Yes. This is a major advantage of using DuploCloud. All controls are mapped to various compliance standards. DuploCloud is also very flexible in enabling you to add custom policies (resource quotas, ability to create public-facing endpoints, etc.)

## Is scaling handled differently from ECS, where you set thresholds and min/max instances to spin up/down?

No. DuploCloud manages to scale in the same way. We expose these thresholds in a simple form that is much easier to configure, even for a user with no DevOps experience. Behind the scenes, DuploCloud maps to the same native AWS constructs.

## Is attaching an RDS instance to each application for spin-up/down purposes expensive? Some of our RDS instances are small.

Small instances are generally no problem. DuploCloud can manage dynamic database spin-up/down with a single RDS database. Sharing AWS services in dynamic environments also helps reduce costs.

## Can an RDS be left intact if I only want to destroy the application and not the database?

Yes.

## Can I upgrade RDS versions?

Yes. Use [AWS Console](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER\_UpgradeDBInstance.Upgrading.html) and see your Cloud Provider for compatibility requirements. Note that while versions 5.7.40, 5.7.41, and 5.7.42 cannot be upgraded to version 8.0.28, you can upgrade these versions to version 8.0.32 and higher.&#x20;

## Is Kubernetes required to use DuploCloud? Is using Kubernetes better than using ECS?

No, Kubernetes is not required. DuploCloud supports both AWS ECS and Kubernetes, among other Cloud solutions.&#x20;

The main advantage of Kubernetes is its broad-based, highly-customizable, third-party open-source community that champions and supports it as a delivery platform. For example, Astronomer (managed air flow), Time series database, IsTio Service Mesh, and Kong API Gateway all expect you to have a Kubernetes deployment. But if your business needs and use cases are met with an AWS solution, for example, you may not need Kubernetes.

Choose the container management software that best satisfies your use cases and the complexity level of your requirements. DuploCloud supports AWS, Kubernetes, Azure, and GCP. Many customers use software from multiple vendors to create robust business solutions backed by DuploCloud's assurance of compliance and automated low-code/no-code DevOps approach.

## Our current RDS logs are sent to CloudWatch. Does DuploCloud support this?&#x20;

Yes.

