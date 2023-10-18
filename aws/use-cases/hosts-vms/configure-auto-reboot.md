---
description: Automatically reboot a host upon StatusCheck faults or Host disconnection
---

# Configure Auto Reboot

Configure hosts to be rebooted automatically if the following occurs:

* **EC2 Status Check** - Applicable for Docker Native and EKS Nodes. The Host is rebooted in the specified interval when a `StatusCheck` fault is identified.&#x20;
* **Kubernetes (K8s) Nodes are disconnected:** Applicable for EKS Nodes only. The Host is rebooted in the specified interval when a `Host Disconnected` fault is identified.

{% hint style="warning" %}
You can configure host Auto Reboot features for a particular Tenant and for a Host.&#x20;

When you configure an Auto Reboot feature for both Tenant _and_ Host, the Host level configuration takes precedence over the configuration at the Tenant level.
{% endhint %}

## Configuring Auto Reboot per Tenant

Use the following procedures to configure Auto Reboot at the Tenant level.

### Configuring Auto Reboot for EC2 Status Check per Tenant

Configure the Auto Reboot feature at the Tenant for Docker Native and EKS Node-based Hosts, to reboot when a `StatusCheck` fault is identified.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenant**. The **Tenant** page displays.
2. Select a Tenant with access to the Host for which you want to configure Auto Reboot.
3. Click the **Settings** tab.
4.  Click **Add**. The **Add Tenant Feature** pane displays.\


    <div align="left">

    <figure><img src="../../../.gitbook/assets/AR100.png" alt=""><figcaption><p><strong>Add Tenant Feature</strong> pane with <strong>Enable Auto Reboot EC2 status check</strong> feature for a <strong>5-</strong>minute interval<br></p></figcaption></figure>

    </div>
5. From the **Select Feature** list box, select **Enable Auto Reboot EC2 status check**.&#x20;
6. In the field below the **Select Feature** list box, enter the time interval in minutes after which the host automatically reboots after a `StatusCheck` fault is identified. Enter zero (**0**) to disable this configuration.
7.  Click **Add**. The configuration is displayed in the **Settings** tab.\


    <div align="left">

    <figure><img src="../../../.gitbook/assets/AR101 (1).png" alt=""><figcaption><p>Tenant <strong>Settings</strong> tab displaying <strong>Enable Auto Reboot EC2 status check</strong> configuration <strong>Value</strong> of <strong>5</strong> minutes</p></figcaption></figure>

    </div>

{% hint style="info" %}
To remove or edit an Auto Reboot Tenant level configuration, click the ( <img src="../../../.gitbook/assets/Kabab_three_Vertical_dots (4).png" alt="" data-size="line"> ) icon and select **Edit Setting** or **Remove Setting**.
{% endhint %}

### Configuring Auto Reboot for Kubernetes (K8s) Node disconnection per Tenant

Configure the Auto Reboot feature at the Tenant for EKS node-based Hosts, to reboot when when a `Host Disconnected` fault is identified is identified.

1. In the DuploCloud Portal, navigate to **Administrator** -> **Tenant**. The **Tenant** page displays.
2. Select a Tenant with access to the Host for which you want to configure Auto Reboot.
3. Click the **Settings** tab.
4. Click **Add**. The **Add Tenant Feature** pane displays.
5. From the **Select Feature** list box, select **Enable Auto Reboot K8s Nodes if disconnected**.&#x20;
6. In the field below the **Select Feature** list box, enter the time interval in minutes after which the host automatically reboots when a `Host Disconnected` fault is identified. Enter zero (**0**) to disable this configuration.
7. Click **Add**. The configuration is displayed in the **Settings** tab.



<figure><img src="../../../.gitbook/assets/AR102.png" alt=""><figcaption><p><strong>Add Tenant Feature</strong> pane with <strong>Enable Auto Reboot K8s Nodes if disconnected</strong> feature for a <strong>3-minute</strong> interval<br></p></figcaption></figure>



<figure><img src="../../../.gitbook/assets/AR103 (1).png" alt=""><figcaption><p>Tenant <strong>Settings</strong> tab displaying <strong>Enable Auto Reboot K8s Nodes if disconnected</strong> configuration <strong>Value</strong> of <strong>3</strong> minutes</p></figcaption></figure>

## Configuring Auto Reboot per Host

Use the following procedures to configure Auto Reboot at the Host level.

### Configuring Auto Reboot for EC2 Status Check per Host

Configure the Auto Reboot feature on the Host level for Docker Native and EKS Node-based Hosts, to reboot when a `StatusCheck` fault is identified.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Hosts**. The **Hosts** page displays.
2. Click the appropriate tab for your Host type and select the Host for which you want to configure Auto Reboot.
3.  Click the **Actions** menu and select **Host Settings** -> **Update Auto Reboot Status Check**. The **Set Auto Reboot Status Check Time** pane displays. \


    <figure><img src="../../../.gitbook/assets/AR104.png" alt=""><figcaption></figcaption></figure>


4. In the Auto Reboot Status Check field, enter the time interval in minutes after which the host automatically reboots after a `StatusCheck` fault is identified. Enter zero (**0**) to disable this configuration.
5. Click **Set**.

### Configuring Auto Reboot for Kubernetes Node disconnection per Host

Configure the Auto Reboot feature on the Host level for EKS node-based Hosts, to reboot when a `Host Disconnected` fault is identified.

1. In the DuploCloud Portal, navigate to **DevOps** -> **Hosts**. The **Hosts** page displays.
2. Click the appropriate tab for your Host type and select the Host for which you want to configure Auto Reboot.
3.  Click the **Actions** menu and select **Host Settings** -> **Update Auto Reboot Disconnected**. The **Set Auto Reboot Status Check Time** pane displays. \


    <figure><img src="../../../.gitbook/assets/AR105.png" alt=""><figcaption></figcaption></figure>


4. In the Auto Reboot Status Check field, enter the time interval in minutes after which the host automatically reboots when a `Host Disconnected` fault is identified. Enter zero (**0**) to disable this configuration.
5. Click **Set**.
