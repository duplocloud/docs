---
description: Using containers and DuploCloud Services with Azure AKS
---

# Containers and Services

## Services <a href="#5-toc-title" id="5-toc-title"></a>

You can deploy any native Docker container in a virtual machine (VM) with the DuploCloud platform. Adding a Service in the DuploCloud Platform is not the same as adding a Kubernetes service.&#x20;

Deploying DuploCloud Services, by clicking the **Add** button in the **AKS/Native** tab, implicitly converts Services into either a deployment set or a StatefulSet. If there are no volume mappings, then the service is mapped to a deployment set. Otherwise, it is mapped to a StatefulSet. Most configuration values are self-explanatory, such as **Images**, **Replicas,** and **Environmental Variables**.

You can supply advanced configuration options in the **Other K8s Config** field. The content of this field maps one-to-one with the Kubernetes API. Configurations for deployment are StatefulSets and are supported by placing the appropriate JSON code in the **Other K8s Config** section. For example, to reference Kubernetes Secrets using a YAML config map, create the following JSON code:&#x20;

```json
"Volumes": [
		{
			"name": "config-volume",
			"configMap": {
				"name": "game-config"
			}
		}
	],
	"VolumesMounts": [
		{
			"name": "config-volume",
			"mountPath": "/etc/config"
		}
	]
}
```

## Adding a DuploCloud Service

1. In the DuploCloud Portal, select **DevOps** -> **Containers** -> **AKS/Native** from the navigation pane.&#x20;
2. Click **Add**. The **Add Service** page displays.
3. Complete the fields on the page, including **Service Name**, **Docker Image** **name**, and number of **Replicas**. Use **Allocation Tags** to deploy the container in a specific set of hosts.&#x20;

{% hint style="warning" %}
Do not use spaces when creating Service or Docker image names.

The number of Replicas that you define must be less than or equal to the number of hosts in the fleet.
{% endhint %}

![DuploCloud Azure Add Service page](../../../.gitbook/assets/Azure\_add\_service2.png)

### Displaying Services <a href="#7-toc-title" id="7-toc-title"></a>

Once the deployment commands run successfully, click the **Services** tile on the **Tenants** page. Your deployments are displayed and you can now attach [load balancers](../load-balancers.md) for the services.

<figure><img src="../../../.gitbook/assets/Azure_tenant_service.png" alt=""><figcaption><p><strong>Tenants</strong> page with <strong>Services</strong> tile</p></figcaption></figure>

## Kubernetes Containers

Using the **Containers** tab in the DuploCloud Portal, you can display and manage the Containers you have defined.

Use the Options Menu ( <img src="../../../.gitbook/assets/Kabab_three_Vertical_dots (1).png" alt="" data-size="line"> ) in each Container row to display **Logs**, **State**, **Container Shell**, **Host Shell,** and **Delete** options.&#x20;

<table><thead><tr><th width="506">Option</th><th>Functionality</th></tr></thead><tbody><tr><td><strong>Logs</strong></td><td>Displays container logs.</td></tr><tr><td><strong>State</strong></td><td>Displays container state configuration, in YAML code, in a separate window.</td></tr><tr><td><strong>Container Shell</strong></td><td>Accesses the Container Shell. To access the <strong>Container Shell</strong> option, you must first set up <a href="../../../aws/prerequisites/kubectl-shell.md">Shell access for Docker</a>.</td></tr><tr><td><strong>Host Shell</strong></td><td>Accesses the Host Shell.</td></tr><tr><td><strong>Delete</strong></td><td>Deletes the container.</td></tr></tbody></table>

<div align="left">

<figure><img src="../../../.gitbook/assets/cont6 (2).png" alt=""><figcaption><p><strong>Containers</strong> tab displaying defined containers with highlighted Options Menu</p></figcaption></figure>

</div>
