---
description: Creating and managing GCP Services using containers
---

# Containers and Services

## Services

Using the **Services** tab in the DuploCloud Portal, you can display and manage the Services you have defined.

Use the Options Menu ( <img src="../../../.gitbook/assets/Kabab_three_Vertical_dots (1).png" alt="" data-size="line"> ) in each Service row to **Edit** or **Delete** Services, as shown below.&#x20;

<figure><img src="../../../.gitbook/assets/cont12.png" alt=""><figcaption><p><strong>Services</strong> tab displaying DuploCloud Services with highlighted Options Menu</p></figcaption></figure>

### Adding Services

#### Docker <a href="#0-toc-title" id="0-toc-title"></a>

You can deploy any native Docker container in a virtual machine (VM) with the DuploCloud platform.&#x20;

1. In the DuploCloud Portal, select **DevOps** -> **Containers** -> **GKE/Native** from the navigation pane.&#x20;
2. Click **Add**. The **Add Service** page displays.
3. Complete the fields on the page, including **Service Name**, **Docker Image** **name**, and number of **Replicas**. Use **Allocation Tags** to deploy the container in a specific set of hosts.&#x20;

{% hint style="info" %}
Do not use spaces when creating Service or Docker image names.

The number of Replicas defined must be less than or equal to the number of hosts in the fleet.
{% endhint %}

<figure><img src="../../../.gitbook/assets/GCP_K8S_Service_Add.png" alt=""><figcaption><p><strong>Add Service</strong> page</p></figcaption></figure>

## Kubernetes Containers

Using the **Containers** tab in the DuploCloud Portal, you can display and manage the Containers you have defined.

Use the Options Menu ( <img src="../../../.gitbook/assets/Kabab_three_Vertical_dots (1).png" alt="" data-size="line"> ) in each Container row to display **Logs**, **State**, **Container Shell**, **Host Shell,** and **Delete** options.&#x20;

<table><thead><tr><th width="374">Option</th><th>Functionality</th></tr></thead><tbody><tr><td><strong>Logs</strong></td><td>Displays container logs.</td></tr><tr><td><strong>State</strong></td><td>Displays container state configuration, in YAML code, in a separate window.</td></tr><tr><td><strong>Container Shell</strong></td><td>Accesses the Container Shell. To access the <strong>Container Shell</strong> option, you must first set up <a href="../../prerequisites/shell-access-for-docker.md">Shell access for Docker</a>.</td></tr><tr><td><strong>Host Shell</strong></td><td>Accesses the Host Shell.</td></tr><tr><td><strong>Delete</strong></td><td>Deletes the container.</td></tr></tbody></table>

<figure><img src="../../../.gitbook/assets/cont9.png" alt=""><figcaption><p><strong>Containers</strong> tab displaying defined containers with highlighted Options Menu</p></figcaption></figure>
