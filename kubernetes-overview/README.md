---
description: Kubernetes features in the DuploCloud Portal
coverY: 0
---

# Kubernetes User Guide

DuploCloud leverages [Kubernetes](https://kubernetes.io/docs/home/) as a foundational building block behind many of its managed Services.

As DuploCloud supports Kubernetes Cluster enablement on all public cloud platforms, you can work with many Kubernetes objects and components. This includes the flexibility to choose the instance type based on workload characteristics, such as compute or memory-intensive tasks and AI/ML workloads that may benefit from GPU instances. It's recommended to have a minimum disk capacity of 40GB per host to accommodate image sizes and application data.

Use the topics in this section to implement many Kubernetes features with little or no hard coding using DuploCloud's no-code/low-code approach. This encompasses configuring autoscaling for your EKS cluster based on CPU/memory usage through Horizontal Pod Autoscaler (HPA) or Auto Scaling Groups (ASG) to scale your Pods or underlying infrastructure as needed efficiently.

For information about cloud-provider-specific Kubernetes container features, see the Kubernetes Containers documentation in the DuploCloud User Guide for your cloud provider. Additionally, DuploCloud can integrate with CloudWatch alarms via the DuploCloud UI to set up custom alerts for CPU/memory usage, ensuring proactive resource monitoring and management. This integration supports forwarding alerts to various notification systems like Sentry, PagerDuty, NewRelic, or OpsGenie for immediate action.

Moreover, when managing your Kubernetes clusters, you can add allocation tags to existing nodes with running services. This action modifies a label on the Kubernetes node, influencing future Pod scheduling without affecting currently running services. The services must be restarted to apply the new allocation tags to existing services. This allows for more granular control over resource allocation and utilization within your cluster.
