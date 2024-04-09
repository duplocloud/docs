# DuploCloud Terraform Provider

The DuploCloud provider offers resources for interacting with the DuploCloud API, facilitating the management of cloud resources through Terraform. For comprehensive documentation, visit:

[https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs](https://registry.terraform.io/providers/duplocloud/duplocloud/latest/docs)

## Retrieving Tenant Security Group ID

When working with DuploCloud and Terraform, you may need to retrieve the tenant security group ID. This can be accomplished by leveraging the AWS security group data source in Terraform, using the security group's name which adheres to the pattern `duploservices-${tenant_name}`. Here's how you can fetch the security group ID:

```terraform
data "aws_security_group" "selected" {
  name = "duploservices-${tenant_name}"
}
```

Once the data source is defined, the security group ID can be accessed with `data.aws_security_group.selected.id`. This approach utilizes the AWS provider's capabilities in Terraform, combined with the predictable naming convention of DuploCloud security groups, to efficiently retrieve the necessary information without direct support from a specific DuploCloud Terraform Provider data source.