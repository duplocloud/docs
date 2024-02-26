---
description: Display logs for the DuploCloud Portal, components, services, and containers
---

# Display logs

## Displaying logs for Service and Tenant with the Central Logging Dashboard

The central logging dashboard displays detailed logs for Service and Tenant.  The dashboard uses Kibana and preset filters that you can modify.

1. In the DuploCloud Portal, navigate to **Observability** -> **Logging**.
2. Select the Tenant from the **Tenant** list box at the top of the DuploCloud Portal.
3. Select the Service from the **Select Service** list box.
4. Modify the **DQL** to customize Tenant selection, if needed.
5. Adjust the date range by clicking **Show dates**.
6. **Add filter**s, if needed.

DuploCloud pre-filters logs per Tenant. All DuploCloud logs are stored in a single index. You can see any Tenant or combination of Tenants (using the DQL option) but the central logging control plane is shared, with no per-Tenant access.&#x20;

{% hint style="success" %}
Confirm that your Hosts and Services are running or runnable to view relevant log data.
{% endhint %}

<figure><img src="../../../.gitbook/assets/screenshot-nimbusweb.me-2024.02.21-14_47_20.png" alt=""><figcaption><p>The Central <strong>Logging</strong> Dashboard in the DuploCloud Portal for a selected Service and Tenant</p></figcaption></figure>

## Displaying Container Logs

See [Kubernetes Containers](../../aws-services/containers/eks-native-containers-and-services.md#kubernetes-containers) for information on displaying logs per container.
