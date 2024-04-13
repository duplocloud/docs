---
description: Create, edit, view, or delete users and assign appropriate roles
---

# Network Segmentation



DuploCloud construct of Infrastructure maps to a VPC in AWS and GCP. In Azure it is VNET. Setting up the network is the starting point and tenants are a child of an infrastructure as shown in the [policy model](../../getting-started/application-focussed-interface/). Kubernetes cluster is tied to the network and part of this setup. For detailed guidance on infrastructure and network setup refer to these individual cloud provider sections ([AWS](../../aws-user-guide/use-cases/disaster-recovery/), [Azure](../../azure-user-guide/use-cases/infrastructure-and-plan/) and [GCP](../../gcp-user-guide/use-cases/disaster-recovery/)) in the guide.&#x20;

Subnets within a network infrastructure are tied to availability zone. A single application's multiple replicas are typically spread across multiple subnets. Subnets thus are not an isloation construct by default. But one can choose to deploy workloads in specific subnets when they launch the virtual machines. In case of Azure subnets also have special considerations are different types of Azure paas services require their own special subnets.\
