---
description: Support Kubernetes Horizontal Pod Autoscaler in the DuploCloud Portal, including handling high memory demands and best practices for autoscaling.
---

# HPA and Handling High Memory Demand

The Kubernetes Horizontal Pod Autoscaler (HPA) is a critical component for managing resources efficiently in a Kubernetes environment. It automatically adjusts the number of pods in a deployment based on observed CPU utilization or other selected metrics. For detailed guidance on autoscaling in Kubernetes, refer to the [Autoscaling in Kubernetes](../aws-user-guide/use-cases/hosts-vms/auto-scaling/kubernetes-scaling-options.md) topic in the AWS DuploCloud documentation.

## Handling High Memory Demand

In instances where a service pod requires more memory than available on any single node, such as a pod demanding 30GB on a node with a maximum of 16GB, it's essential to isolate the resource-intensive service. By moving the script causing high memory demand to its own service and allocating it to a larger instance with a `highmem` allocation tag, you can ensure that your services continue to run efficiently. This approach allows for the use of instances with up to 64GB of memory, accommodating high-demand applications without compromising the performance of other services.

## Best Practices for Autoscaling

When configuring autoscaling for an EKS cluster, it's crucial to base the autoscaler on CPU/memory requests or limits to ensure optimal performance and resource utilization. This method allows for dynamic scaling that responds to the actual needs of your applications, preventing over-provisioning and resource wastage.

## Custom Monitoring and Alerts

For advanced monitoring and alerting, DuploCloud supports the integration of its Prometheus endpoints with external Grafana instances. This capability enables the setup of custom alerts for memory usage by pod, allowing for proactive resource management and issue resolution. Whether using DuploCloud's Grafana instance or an external one, these integrations provide valuable insights into your Kubernetes environment's health and performance.

## Considerations for Allocation Groups

Adding an allocation group to an existing node with running services requires careful consideration regarding service continuity and the potential need for restarts. While the specific behavior may vary, understanding the implications of such changes is crucial for maintaining uninterrupted service availability during scaling and resource adjustments.

By following these guidelines and leveraging DuploCloud's support for HPA, teams can effectively manage Kubernetes resources, ensuring that applications remain performant and resilient under varying loads.