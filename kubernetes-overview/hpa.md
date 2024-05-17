---
description: Manage and troubleshooting services with HPA configured.
---

# HPA

## Using the Horizontal Pod Autoscalar (HPA) in AWS

See the [Autoscaling in Kubernetes](../overview/use-cases/hosts-vms/auto-scaling/kubernetes-scaling-options.md) topic in the AWS DuploCloud documentation.

## Managing Services with HPA

When working with Kubernetes services configured with Horizontal Pod Autoscaler (HPA), it's essential to understand how to manage and troubleshoot them effectively.

### Stopping a Service with HPA

To stop a service that is hung in a Running state due to HPA, you cannot directly delete pods, as new ones are created to maintain the set number of replicas. Instead, remove the HPA configuration and adopt a static replication strategy by setting the replica count to 0. This ensures the service is effectively stopped without attempting to set `minReplicas` to 0, which is an invalid configuration for HPA.

### Troubleshooting

If issues arise while stopping a service with HPA configured, avoid setting `minReplicas` it to 0 and ensure the HPA configuration is removed in favor of a static replication strategy. For further troubleshooting, consult the Faults menu under the DevOps section in the DuploCloud UI, where all errors are logged, facilitating efficient diagnosis and resolution.

### UI Improvements

DuploCloud is planning enhancements to the UI to improve the management of services running with HPA configurations. These improvements include adding validation to prevent set `minReplicas` to 0, potentially removing the `Stop` option for services with HPA, and documenting the correct procedure for stopping such services. These updates simplify the process and prevent common configuration mistakes, ensuring a smoother experience managing Kubernetes services with HPA.

## HPA and Handling High Memory Demand

See the Autoscaling in Kubernetes topic in the AWS DuploCloud documentation. The Kubernetes Horizontal Pod Autoscaler (HPA) is critical for managing resources efficiently in a Kubernetes environment. It automatically adjusts the number of pods in a deployment based on observed CPU utilization or other selected metrics. For detailed guidance on autoscaling in Kubernetes, refer to the Autoscaling in Kubernetes topic in the AWS DuploCloud documentation.

### Handling High Memory Demand

In instances where a service pod requires more memory than is available on any single node, such as a pod demanding 30GB on a node with a maximum of 16GB, it's essential to isolate the resource-intensive service. By moving the script, which causes high memory demand for its service, and allocating it to a more prominent instance with an `highmem` allocation tag, you can ensure that your services continue to run efficiently. This approach allows for instances with up to 64GB of memory, accommodating high-demand applications without compromising the performance of other services.

### Best Practices for Autoscaling

When configuring autoscaling for an EKS cluster, it's crucial to base the autoscaler on CPU/memory requests or limits to ensure optimal performance and resource utilization. This method allows for dynamic scaling that responds to the actual needs of your applications, preventing over-provisioning and resource wastage.

### Custom Monitoring and Alerts

For advanced monitoring and alerting, DuploCloud supports the integration of its Prometheus endpoints with external Grafana instances. This capability enables the pod to set up custom alerts for memory usage, allowing for proactive resource management and issue resolution. Whether using DuploCloud's Grafana instance or an external one, these integrations provide valuable insights into your Kubernetes environment's health and performance.

### Considerations for Allocation Groups

Adding an allocation group to an existing node with running services requires careful consideration regarding service continuity and the potential need for restarts. While the specific behavior may vary, understanding the implications of such changes is crucial for maintaining uninterrupted service availability during scaling and resource adjustments.

By following these guidelines and leveraging DuploCloud's support for HPA, teams can effectively manage Kubernetes resources, ensuring that applications remain performant and resilient under varying loads.
