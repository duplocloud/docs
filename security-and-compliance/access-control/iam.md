# IAM

Access to many PAAS services by cloud providers are not network policy based but based on the provider's IAM framework. For example in AWS it is IAM polcies, in Azure its via managed identities and in GCP it is via service accounts. Similarly in a Kubernetes cluster it is via service accounts.

DuploCloud tenant is an IAM boundry. Any PAAS resource within a tenant is automatically accessed by any compute workload via IAM. For example:

* In AWS each tenant is an IAM role and compute like VM, Lambda functions, EMR, Airflow JOBs etc are given the IAM role which in turn is configured to have access to all PAAs services in that tenant like  S3 buckets, DynamoDB tables, secrets manager, SSM parameter, SQS queues etc.
* In Azure each tenant is a managed identity and compute like VM, Functions etc are attached with this managed identity which in turn is configured to have access all PAAS services in that tenant like Azure storage, Keyvault etc.&#x20;
* In GCP each tenant is a service account and compute like VM, functions etc are attached to this service account  which in turn is configured to have access all PAAS services in that tenant like cloud storage, pubsub etc.
