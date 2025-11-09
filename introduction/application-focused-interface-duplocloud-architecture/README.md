---
description: >-
  A high-level overview of the building blocks of DuploCloud's
  infrastructure-based architecture
---

# Policy Model

The DuploCloud Policy Model is an application-infrastructure-centric abstraction created atop the user's cloud provider account. The following diagram shows the abstractions within which applications are deployed, and users operate. Below bullet points are a brief introduction to the concepts and subsequent sub sections explain this in details

* **DuploCloud Platform** installs in customer's cloud account. In case of Azure and GCP a single instance can manage multiple subscriptions and GCP projects respectively. In case of AWS we need one agent per AWS account but they come together in a federated fashion to expose a single interface. This is described more in detail under the Management Portal Scope [Section below](management-portal-scope.md)
* **Infrastructure**: An infrastructure maps to a VPC in a region with optionally a Kubernetes Cluster. One cloud account (AWS account, GCP project or Azure subscription) can have multiple infrastructures (1:N). For more details of infrastructure see [here](./).
* **Plan**: When you create an[ Infrastructure](infrastructure.md) in DuploCloud, a Plan is automatically generated. A Plan is a placeholder or a template for configurations. These configurations are consistently applied to all Tenants within the Plan (or Infrastructure). For more details of Plan [see here](plan.md)
* **Tenant** is like an environment and is a child of the Infrastructure. It is the most fundamental construct in DuploCloud. While Infrastructure is a VPC level isolation, Tenant is the next level of isolation implemented by segregating Tenants using concepts like Security Groups, IAM roles, Instance Profiles, K8S Namespaces, KMS Keys, etc. For more details of Tenant see the [following section](tenant.md)

<div data-full-width="true"><figure><img src="../../.gitbook/assets/Screenshot (786).png" alt=""><figcaption><p>A diagram of DuploCloud application deployment</p></figcaption></figure></div>
