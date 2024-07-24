# DuploCloud Architecture: an Application Focused Interface

The DuploCloud platform is an application infrastructure-centric abstraction created on top of the user's cloud provider account. Users can deploy and operate their applications using DuploCloud's simple, user-friendly UI, or use the low-code Terraform provider to consume cloud services like S3, DynamoDB, Lambda functions, GCP Redis, Azure SQL, etc., from their cloud provider.

Since DuploCloud is a self-hosted platform running in the customer's cloud account, the platform can work in tandem with direct changes on the cloud account. This means that while some security functions (IAM roles, KMS keys, Azure Managed Identities, GCP service accounts, etc.) are hidden from the end user, they are still configurable. This is explained with examples at [https://duplocloud.com/white-papers/devops/](https://duplocloud.com/white-papers/devops/).

The following diagram shows the high-level abstractions within which applications are deployed, and users operate.

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-31 17321600000.jpg" alt=""><figcaption><p>DuploCloud Application Deployment</p></figcaption></figure>
