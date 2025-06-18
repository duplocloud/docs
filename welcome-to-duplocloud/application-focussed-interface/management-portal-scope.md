---
description: >-
  An overview of the scope of cloud provider resources (accounts) that a
  DuploCloud Portal can manage
---

# Management Portal Scope

Following is the scope of cloud provider resources (accounts) that a single DuploCloud Portal can manage:

**Azure**: A single DuploCloud Portal can manage multiple Azure subscriptions. Azure has native identity services like Azure Active Directory (Azure AD) and Entra ID, which provide managed identities that can be granted access across multiple subscriptions. DuploCloud inherits the permissions of these managed identities, allowing it to seamlessly access and manage resources across the Azure subscriptions it is connected to.

**GCP**: Similar to Azure, a single instance of DuploCloud can manage multiple GCP projects.

**AWS**: In AWS a single DuploCloud Portal manages one and only one AWS account. This is inline with the AWS IAM implementation i.e. even in native AWS IAM model the building blocks like IAM role, Instance profiles do not span multiple accounts. The cross account SCP policies are quite light weight. In fact AWS organizations was added almost 10 years after the launch of AWS. For example, when a user logs in using AWS Identity center, they have to choose an account and the session is scoped to that. See the picture below of the IAM login console.\
\
![](<../../.gitbook/assets/image (1) (3).png>)

We implement the same experience, providing an account switcher on the login page and inside the Portal, as shown below. For instructions on adding additional login portals to the DuploCloud login screen, see the [Multiple Portal Login Options pag](../../access-control/multiple-portal-login-options.md)e.\
&#x20;&#x20;

<figure><img src="../../.gitbook/assets/image (2) (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3) (3).png" alt=""><figcaption></figcaption></figure>
