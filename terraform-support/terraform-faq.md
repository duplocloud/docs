# Terraform FAQ

## 1 . Terraform vs. CDK

For implementing Infrastructure as Code (IaC), DuploCloud integrates well with Terraform and CDK scripts. However, Terraform offers distinct advantages, including its broader vendor support and the ease of maintaining infrastructure with a single language across different tools and services. Terraform's extensive community support and compatibility with various open-source tools make it a preferred choice for many developers.

### Integration Details

* **Terraform**: DuploCloud provides a Terraform provider that makes it straightforward to utilize DuploCloud's security constructs, such as tenant IAM roles, instance profiles, and KMS keys. This ensures that resources created via Terraform can fully leverage DuploCloud's security features.
* **CDK**: DuploCloud's security constructs must be manually referenced in the CDK scripts for resources created with CDK. Despite this, DuploCloud's security monitoring capabilities remain effective across all resources, ensuring compliance and security regardless of the IaC tool used.

### Key Differences

The fundamental difference between using Terraform and CDK with DuploCloud lies in managing security constructs and variable referencing. Terraform allows for direct referencing of DuploCloud's security constructs, making it more efficient for managing credentials and configurations. In contrast, CDK requires manual input of these constructs, which can be less efficient. Despite these differences, both Terraform and CDK are viable options for integrating with DuploCloud, with Terraform being the preferred choice due to its broader support and versatility.\`
