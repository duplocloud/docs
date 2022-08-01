# Tenant (Environment)

Tenant is the most foundational concept in DuploCloud platform. Tenant is like an environment.&#x20;

![](<../../.gitbook/assets/image (16) (2).png>)

Tenant is fundamentally the following things at the logical level:

* _Container of resources_: All resources (except ones corresponding to infrastructure) are created within the Tenant. If we delete the tenant then all resources within that are terminated.
* _Security Boundary_: All resources within the tenant can talk to each other. For example a Docker container deployed in an EC2 instance within the tenant will have access to S3 buckets and RDS instances within the same tenant. RDS instances in another tenant cannot be reached, by default. Tenant can expose endpoints to each other either via load balancers or explicit inter-tenant security groups and IAM policies.
* _User Access Control:_ Self-service is the bedrock of the DuploCloud platform. To that end, users can be granted Tenant level access. For example John and Jim are developers who can be granted access to Dev tenant, while Joe is an administrator who has access to all tenants, while Anna is a data scientist who has access only to the data science tenant.
* _Billing Unit:_ Since Tenant is a container of resources, all resources in the tenant are tagged with the Tenant's name in the cloud provider, making it easy to segregate usage by tenant.
* Alerting: All alerts that represent everything wrong with any resource within the Tenants
* Central Logging per Tenant: There a logs view per tenant
* Metrics: There is a Metrics view per Tenant



Following are a few ways one can use the Tenant concept

* A user can map Tenants to say one each of all their DEV, Test, Stage, QA and Prod.&#x20;
* A use case where there are a large set of applications worked upon by different teams, in that case Tenant could be mapped to an environment where an environment maps to the team's workloads say dev-analytics, stage-analytics, dev-fe, prod-fe.&#x20;
* The company may have a "Single Tenant (not to be confused with DuploCloud Tenant) Enterprise application" where per end client of theirs they create a new environment. In that case a DuploCloud Tenant would map to an Environment for the end client. &#x20;



While Infrastructure is a VPC and Kubernetes/ECS Cluster level isolation, Tenant is the next level of isolation implemented in AWS by segregating Tenants using the following construct _per_ Tenant

* A set of Security Groups
* 1 IAM role and Instance Profile.
* 1 K8S Namespace, 1 read-only service account, 1 write service account
* 1 KMS Key
* 1 PEM Key
* There may be other per service constructs.

EKS Worker nodes or VMs that are created within a tenant are marked with a "label" with Tenant Name. By default when apps are deployed in this tenant, the node selector with the same label i.e. the tenant name is placed on them in addition to placing them in the Tenant's namespace. Thus even at the worker node level two tenants are completely isolated even though they maybe sharing the same Kubernetes cluster control by virtue of a shared Infrastructure&#x20;
