# DuploCloud Terraform Provider

The DuploCloud provider offers a seamless way to interact with the DuploCloud API, facilitating the integration of AWS Security Hub and the management of infrastructure using Terraform (TF) and AWS Cloud Development Kit (CDK). This integration not only enhances security through a built-in Security Information and Event Management (SIEM) system but also supports the attachment of new AWS accounts to the AWS Security Hub directly, typically recommended for production environments to optimize costs.

## AWS Security Hub Integration

DuploCloud supports AWS Security Hub integration out of the box, enabling users to easily attach new accounts to their AWS Security Hub. This feature is particularly useful in production accounts, allowing for cost savings by avoiding the activation of this service in non-production environments.

## Terraform vs. CDK

When it comes to Infrastructure as Code (IaC), DuploCloud integrates well with both Terraform and CDK scripts. However, there are distinct advantages to using Terraform, including its broader vendor support and the ease of maintaining infrastructure with a single language across different tools and services. Terraform's extensive community support and compatibility with various open-source tools make it a preferred choice for many developers.

### Integration Details

- **Terraform**: DuploCloud provides a Terraform provider that makes it straightforward to utilize DuploCloud's security constructs, such as tenant IAM roles, instance profiles, and KMS keys. This ensures that resources created via Terraform can fully leverage DuploCloud's security features.
- **CDK**: For resources created with CDK, DuploCloud's security constructs must be manually referenced in the CDK scripts. Despite this, DuploCloud's security monitoring capabilities remain effective across all resources, ensuring compliance and security regardless of the IaC tool used.

### Key Differences

The fundamental difference between using Terraform and CDK with DuploCloud lies in the management of security constructs and variable referencing. Terraform allows for direct referencing of DuploCloud's security constructs, making it more efficient for managing credentials and configurations. In contrast, CDK requires manual input of these constructs, which can be less efficient. Despite these differences, both Terraform and CDK are viable options for integrating with DuploCloud, with Terraform being the preferred choice due to its broader support and versatility.

For more detailed documentation on the DuploCloud Terraform provider, visit:

[https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs)