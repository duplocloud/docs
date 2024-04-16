---
description: Kubernetes features in the DuploCloud Portal
coverY: 0
---

# Kubernetes Overview

DuploCloud leverages [Kubernetes](https://kubernetes.io/docs/home/) as a foundational building block behind many of its managed Services.&#x20;

As DuploCloud supports Kubernetes Cluster enablement on all public cloud platforms, there are many Kubernetes objects and components that you can work with. This includes the flexibility to choose the instance type based on workload characteristics, such as compute or memory-intensive tasks, and AI/ML workloads which may benefit from GPU instances. It's recommended to have a minimum disk capacity of 40GB per host to accommodate image sizes and application data.

Use the topics in this section to implement many Kubernetes features with little or no hard coding, using DuploCloud's no-code/low-code approach. This encompasses configuring autoscaling for your EKS cluster based on CPU/memory usage through Horizontal Pod Autoscaler (HPA) or Auto Scaling Groups (ASG) to efficiently scale your pods or underlying infrastructure as needed.

For information about public-cloud provider-specific Kubernetes container features, see the [Kubernetes Containers documentation](../aws-user-guide/aws-services/containers/eks-containers-and-services.md#kubernetes-containers) in AWS EKS, for example. Additionally, DuploCloud can integrate with CloudWatch alarms via the DuploCloud UI for setting up custom alerts for CPU/memory usage, ensuring proactive monitoring and management of resources. This integration supports forwarding alerts to various notification systems like Sentry, PagerDuty, NewRelic, or OpsGenie for immediate action.

Moreover, when managing your Kubernetes clusters, it's possible to add allocation tags to existing nodes with running services. This action modifies a label on the Kubernetes node, influencing future pod scheduling without affecting currently running services. To apply the new allocation tags to existing services, a restart of the services is required, allowing for more granular control over resource allocation and utilization within your cluster.