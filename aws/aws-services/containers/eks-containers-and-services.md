# EKS Containers and Services

## Adding a DuploCloud EKS/Native Service

1. In the DuploCloud Portal, select **DevOps** -> **Containers** -> **EKS/Native** from the navigation pane.&#x20;
2. Click **Add**. The **Add Service** page displays.
3. Complete the fields on the page, including **Service Name**, **Docker Image** **name**, and number of **Replicas**. Use **Allocation Tags** to deploy the container in a specific set of hosts.&#x20;
4. To force the creation of Kubernetes StatefulSets, select **Yes** in the **Force StatefulSets** field.

{% hint style="warning" %}
Do not use spaces when creating Service or Docker image names.

The number of Replicas you define must be less than or equal to the number of hosts in the fleet.
{% endhint %}

<div align="left">

<img src="../../../.gitbook/assets/k8_statefulSet_force.png" alt="Add Service page">

</div>

{% hint style="info" %}
If custom `allocationtag` and `tenantname` is specified in the `NodeSelector` section of **Other Pod Config**, values will be ignored. These are the reserved keys by DuploCloud
{% endhint %}
