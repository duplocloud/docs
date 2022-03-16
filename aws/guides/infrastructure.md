# Infrastructure

A completely new isolated environment can be created for use cases from DuploCloud. Proceed to **Administrator → Infrastructure**. Click on +Add button. It opens a form where it asks to enter basic information about the new environment.

![](https://duplocloud.com/wp-content/uploads/2021/11/create-infra.png)

Once you submit the form, DuploCloud creates a new VPC with 2 subnets (private, public) in each availability zone, necessary security groups, NAT Gateway, Internet Gateway, Route tables, etc. DuploCloud also configures the VPC peering with the master VPC which is initially configured in DuploCloud. Infrastructure creation takes around 10mins to complete. Once it's complete, a new plan with the same infrastructure name is automatically created and populated with the details of the newly created infrastructure. This plan can then be used to create the tenants.

![](https://duplocloud.com/wp-content/uploads/2021/11/infra-plan.png)
