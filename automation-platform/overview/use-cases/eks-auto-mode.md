---
description: Using EKS Auto Mode with DuploCloud.
---

# EKS Auto Mode

[EKS Auto Mode](https://aws.amazon.com/eks/auto-mode/) is a simplified, fully managed option for deploying Kubernetes clusters in DuploCloud using Amazon Elastic Kubernetes Service (EKS). With Auto Mode, AWS handles node provisioning, scaling, and lifecycle management, reducing operational overhead for faster, hands-off cluster deployments.

EKS Auto Mode is ideal if you:

* Want fast, low-maintenance EKS cluster setup.
* Do not need SSH access to worker nodes.
* Do not require custom AMIs.
* Prefer automated autoscaling and lifecycle management via AWS Karpenter.

See the table below for a detailed comparison of **EKS Auto Mode** and **EKS Standard Mode** to help you choose the best option for your use case.

{% hint style="danger" %}
**Important:** DuploCloud does **not support switching between Auto Mode and Standard Mode** after an infrastructure is created. Changing the mode may require you to delete and recreate the infrastructure. Choose carefully based on your project requirements.
{% endhint %}

| **Category**                                   | **EKS Standard Mode**                                                                                                                                                                                                                                                      | **EKS Auto Mode**                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Custom AMIs**                                | Supports custom AMIs                                                                                                                                                                                                                                                       | Not supported. AWS manages AMIs, which are immutable                                                                                                                                                                                                                                                                                                                           |
| **Host Access**                                | Full host access via SSH.  Users manage nodes directly                                                                                                                                                                                                                     | No SSH access: cannot install custom software on nodes                                                                                                                                                                                                                                                                                                                         |
| **Node Management and Scaling**                | <p>No out-of-the-box solution:<br>- Requires manual setup of Auto Scaling Groups (ASGs) and node groups.<br>- One instance type per node group.<br>- Node cycling is manual unless scaling or upgrading.<br>- DuploCloud provides optional cluster autoscaler setting.</p> | <p>Fully automated via Karpenter: <br>- No need to configure ASGs or node groups.<br>- Supports multiple instance types, families, and hardware.<br>- Mandatory node cycling every 21 days.<br>- Built-in cost optimization and dynamic scaling.<br>- Works out of the box with no extra configuration.<br>- DuploCloud preserves tenant network and permission isolation.</p> |
| **Load Balancing**                             | <p>Load Balancer Controller available via infra setting.<br><br>Network Load Balancers are not supported.</p>                                                                                                                                                              | <p>Load Balancer Controller included by default: no setup.</p><p><br>Network Load Balancers are not supported.</p>                                                                                                                                                                                                                                                             |
| **Storage**                                    | <p>EBS CSI driver installed and managed by DuploCloud.<br><br>EFS is supported.</p>                                                                                                                                                                                        | <p>EBS CSI driver installed and managed by AWS.<br><br>EFS is supported.</p>                                                                                                                                                                                                                                                                                                   |
| **EKS Upgrades**                               | DuploCloud orchestrates control plane upgrades and manages version cycling for plugins and nodes.                                                                                                                                                                          | DuploCloud upgrades the control plane only; AWS Auto Mode handles plugin and node version cycling.                                                                                                                                                                                                                                                                             |
| **AOS (Advanced Observability Stack) Support** | Fully supported, tested, and stable.                                                                                                                                                                                                                                       | Beta: should work with privileged containers, but not yet considered stable.                                                                                                                                                                                                                                                                                                   |
| **Cost and Billing**                           | Lower cost. You pay only for EC2 and EBS resources                                                                                                                                                                                                                         | Higher cost. You pay AWS Auto Mode node fees on top of EC2 and EBS.                                                                                                                                                                                                                                                                                                            |

## Creating an Infrastructure with EKS Auto Mode

To create an infrastructure using EKS Auto Mode:

1. In the DuploCloud Portal, navigate to **Administrator** → **Infrastructure**.
2.  Click **Add**. The **Add Infrastructure** pane displays.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot (733).png" alt=""><figcaption></figcaption></figure>
3. Complete the fields, being sure to:
   * Check **Enable EKS**.&#x20;
   * Set **Cluster Mode** to **EKS Auto Mode**.
4. Configure additional fields such as region, VPC CIDR, availability zones, etc., as needed.
5. Click **Create**.

For more details about creating an infrastructure, see [Creating an Infrastructure and Plan for AWS](../../../overview/use-cases/creating-an-infrastructure-and-plan-for-aws/).

{% hint style="info" %}
**Note:** After creating an Auto Mode Tenant, there is a brief warm-up period (2–3 minutes) before Karpenter becomes fully active.&#x20;
{% endhint %}

## Creating Node Pools

In EKS Auto Mode, creating one or more node pools is essential for provisioning worker nodes to run your Kubernetes workloads. Node pools define the compute resources and scheduling constraints for your cluster’s nodes.

For detailed instructions on creating and managing node pools, see the [DuploCloud Node Pools documentation](../../kubernetes-overview/node-pools.md).&#x20;

## Additional Resources

* [Creating Node Pools](../../overview-1/gcp-services/node-pools.md): Create and manage node pools.
* [Create a Tenant](tenant-environment/): Set up a workspace within the infrastructure to organize your application resources.
* [Create an EKS Service](../aws-services/containers/eks-containers-and-services/#creating-a-duplocloud-eks-service): Deploy a Kubernetes workload to your Auto Mode cluster by creating services that manage and expose your applications within the cluster.
