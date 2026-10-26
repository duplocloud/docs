---
description: Managing Azure services and related components
---

# Azure Services

DuploCloud provides a number of configurable components when running Microsoft Azure's Managed Kubernetes Service (AKS).

Applications involve many Azure Services like Storage Account, RDS for RDBS (MySQL), Redis, VM Scale Sets, Ingress, ALB/NLB load balancers, and so on. While each of their configurations needs a few application-centric inputs, there are scores of lower-level nuances around access control, security, and compliance.

Using DuploCloud you can create virtually any service within the Tenant using basic application-centric inputs. At the same time, the platform will make sure the lower-level nuances are programmed to best practices for security and compliance.

## Supported Services for DuploCloud Azure

Supported Services are listed in alphabetical order, following the core services: Containers, and Load Balancers

### Core Services

* [Containers and Services](containers-and-services/)
* [Load Balancers](load-balancers.md)

### Additional Services

* [​Agent Pools](agent-pool/)
* [AKS Shared Application Gateway](../../kubernetes-overview/ingress-loadbalancer/aks-ingress/)
* [Azure Container Apps​](azure-container-apps.md)
* [Azure Container Registry (ACR)](azure-container-registry-acr.md)
* ​[Databases](databases/)
  * [MSSQL](databases/sql-database.md)
  * [PostgreSQL database](databases/postgresql.md)
  * [PostgreSQL Flexible Server](databases/postgresql-flexible-server.md)
  * [MySQL Server database](databases/mysql-server-database/)
    * [Azure Managed SQL Instances](databases/mysql-server-database/azure-managed-instance.md)
  * [MySQL Flexible Server](databases/mysql-flexible-server.md)
  * [Redis database](databases/redis-database.md)
  * [CosmosDB](databases/cosmosdb.md)
* [Databricks](databricks.md)
* ​[Data Factory​](data-factory.md)
* ​[Docker Web Application](docker-web-application.md)
* [Infra Secrets​](infra-secrets.md)​
* [​Key Vault​](key-vault.md)
* ​[Public IP Address Prefix​](public-ip-address-prefix.md)
* [​Serverless](web-applications/)
  * [App Service Plans and Web Apps](web-applications/app-service-plans-and-web-apps.md)
  * [Function Apps​](web-applications/functions.md)
* [​Service Bus​](service-bus.md)
* [​Storage Account​](storage-account.md)
* [​Subscription​](subscription.md)
* ​[VM Scale Sets](vm-scale-sets.md)
