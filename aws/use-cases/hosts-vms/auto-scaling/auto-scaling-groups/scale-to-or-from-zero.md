---
description: Scale to or from zero when creating Autoscaling Groups in DuploCloud
---

# Scale to or from Zero

DuploCloud allows you to scale to or from zero in EKS clusters by enabling the **Scale from zero** option in the Advanced Options when creating an [Autoscaling Group](../../../auto-scaling/auto-scaling-groups.md).

Scaling to or from zero with AWS Autoscaling Groups (ASG) offers several advantages depending on the context and requirements of your application:

## Advantages of Scaling to Zero

* **Cost Savings**: By scaling down to zero instances during periods of low demand, you minimize costs associated with running and maintaining instances. This pay-as-you-go model ensures you only pay for resources when they are actively being used.
* **Resource Efficiency**: Scaling to zero ensures that resources are not wasted during periods of low demand. By terminating instances when they are not needed, you optimize resource utilization and prevent over-provisioning, leading to improved efficiency and reduced infrastructure costs.
* **Flexibility**: Scaling to zero provides the flexibility to dynamically adjust your infrastructure in response to changes in workload. It allows you to efficiently allocate resources based on demand, ensuring that your application can scale up or down seamlessly to meet varying levels of traffic.
* **Simplified Management**: With automatic scaling to zero, you can streamline management tasks associated with provisioning and de-provisioning instances. The ASG handles scaling operations automatically, reducing the need for manual intervention and simplifying infrastructure management.

## Advantages of Scaling from Zero

* **Rapid Response to Increased Demand**: Scaling from zero allows your infrastructure to quickly respond to spikes in traffic or sudden increases in workload. By automatically launching instances as needed, you ensure that your application can handle surges in demand without experiencing performance degradation or downtime.
* **Improved Availability**: Scaling from zero helps maintain optimal availability and performance for your application by ensuring that sufficient resources are available to handle incoming requests. This proactive approach to scaling helps prevent resource constraints and ensures a consistent user experience even during peak usage periods.
* **Enhanced Scalability**: Scaling from zero enables your infrastructure to scale out horizontally, adding additional instances as demand grows. This horizontal scalability allows you to seamlessly handle increases in workload and accommodate a growing user base without experiencing bottlenecks or performance issues.
* **Elasticity**: Scaling from zero provides elasticity to your infrastructure, allowing it to expand and contract based on demand. This elasticity ensures that you can efficiently allocate resources to match changing workload patterns, resulting in optimal resource utilization and cost efficiency.

\
