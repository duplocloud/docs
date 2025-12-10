# Shared Hosts

Shared Hosts allow workloads to run on the same set of virtual machines (VMs), making better use of resources across multiple Tenants. DuploCloud supports Services, Jobs, and CronJobs on Shared Hosts in Azure, providing flexibility for running long-running services, batch jobs, and scheduled tasks.

DuploCloud supports Shared Hosts for:

* Services
* Jobs
* CronJobs

## Configuring Tenants to Allow Host Sharing

To enable Host sharing, configure one Tenant to share its Hosts, and another Tenant to run K8s Pods on any Host.

### **Enabling a Tenant to Share its Hosts**

1. In the DuploCloud Portal, go to **Administrator** → **Tenant**.
2. From the Tenant list box, select the Tenant that will share its Host.
3. Click the **Settings** tab.
4.  Click **Add**. The **Add Tenant Feature** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/image (482).png" alt="" width="455"><figcaption><p><strong>Add Tenant Feature</strong> pane</p></figcaption></figure></div>
5. From the **Select Feature** list, select **Allow hosts to run K8S pods from other tenants**.
6. Select **Enable**, then click **Add**. This Tenant's Hosts (Azure VMs) can now run Pods from other Tenants.

### **Enabling a Tenant to Run Pods on Shared Hosts**

1. In the DuploCloud Portal, go to **Administrator** → **Tenant**.
2. Select the Tenant that will run Pods on the shared Host.
3. Click the **Settings** tab.
4.  Click **Add**. The **Add Tenant Feature** pane displays.<br>

    <div align="left"><figure><img src="../../../../.gitbook/assets/image (483).png" alt="" width="455"><figcaption><p><strong>Add Tenant Feature</strong> pane</p></figcaption></figure></div>
5. From the **Select Feature** list, select **Enable option to run K8S pods on any host**.
6. Select **Enable**, then click **Add**. This Tenant can now run Pods on other Tenant's Hosts.

## Creating Services, Jobs, and CronJobs on Shared Hosts

After configuring Tenant settings to allow Host sharing, create the resources you want to run on the Shared Hosts.

### **Creating a Service to Run on a Shared Host**

1. From the Tenant list, select the Tenant that will run Pods on the Shared Host.
2. Go to **Kubernetes → Services**.
3.  Click **Add**. The **Add Service** page displays.<br>

    <figure><img src="../../../../.gitbook/assets/Screenshot (153).png" alt=""><figcaption><p>The <strong>Add Service</strong> page</p></figcaption></figure>
4.  Fill in the **Service Name**, **Cloud**, **Platform**, and **Docker Image** fields. Click **Next**.<br>

    <figure><img src="../../../../.gitbook/assets/Screenshot (154).png" alt=""><figcaption><p>The <strong>Add Service</strong> <strong>Advanced Options</strong> page</p></figcaption></figure>
5. Enable **Run on Any Host**.
6. Click **Create**. A Service running on the shared Host is created.

### **Creating a Job or CronJob to Run on a Shared Host**

Before creating a Kubernetes Job or CronJob to run on a Shared Host, [configure Tenant settings to allow Host sharing](../../../overview/use-cases/hosts-vms/adding-shared-hosts.md#configuring-tenants-to-allow-host-sharing).&#x20;

Once Host sharing is enabled:

1. Follow the steps in the DuploCloud documentation to [create a Kubernetes Job](../../../kubernetes-overview/jobs.md#creating-a-kubernetes-job-in-the-duplocloud-portal) or [create a Kubernetes CronJob](../../../../kubernetes/cronjobs.md#creating-a-kubernetes-cronjob-in-the-duplocloud-portal).
2. On the **Add Kubernetes Job** or **Add Kubernetes CronJob** page, enable the **Run on Any Host** option.
3. Click **Create** to deploy the Job or CronJob on a Shared Host.
