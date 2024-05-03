# Agent Management

Agents are typically required to be installed on virtual machines so they can collect data and send it to their respective controlling software running in a central location. For example, Ossec is the agent for the SIEM Wazuh. Crowdstrike and Laceworks all have their respective agents. ClamAV anti-virus can also be considered an agent whose results we collect and send to Wazuh.

DuploCloud platform provides seamless installation and management of these agents. There are 3 types of agents that we install:

* Docker-based agents
  * The Kubernetes DaemonSet runs in all or a subset of hosts in a cluster. Typically these containers are launched with privileged access over the host operating system
  * Containers that run on all or a subset of hosts are orchestrated through DuploCloud's built-in container orchestration. Typically, these containers are launched with predefined access to the host operating system.
* Non-Docker VM agents are Linux packages or Windows services that are installed and baked in virtual machine images before they are launched. They can also be installed via user data.&#x20;

## Agent Setup&#x20;

1.  **Create an Agent Type.** Each vendor or agent software is considered a type. For example, Ossec, Clamav, Laceworks, and Crowdstrike are all different agent types. To add a new agent type, navigate to **Security** -> **Agents** and click **Add.** The **Add Security Agent** pane displays. Enter the **Agent Name** and click **Create**.\


    <figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p><strong>Add Security Agent</strong> pane.</p></figcaption></figure>


2. **Create an agent deployment.** Under the desired **Agent** tab, **Add** a deployment to deploy the agent to the Hosts. You must deploy at least one agent per Kubernetes cluster. You can deploy on all hosts in a Kubernetes cluster, or you can deploy on all hosts for a specific Tenant. Deploying on all hosts for one Tenant is useful for certain Kubernetes clusters or DuploCloud Infrastructures where you have Tenants on which you don't want specific agents to be run.&#x20;

{% hint style="info" %}
Behind the scenes, this deployment is just a regular Kubernetes Daemonset deployment or a built-in container orchestration deployment within a tenant, as documented here.&#x20;
{% endhint %}

## Creating multiple deployments for multiple Tenants&#x20;

You can create multiple deployments for multiple tenants. In the case of Kubernetes-based container orchestration, as against Duplocloud built-in orchestration, with just one deployment, you can target all nodes in the cluster. The following are the fields in the **Update Security Agent Deployment** page:

* **Name** is a desired name to track the deployment.
* **Cluster** is the infrastructure name and is the maximum scope of deployment.&#x20;
* **Host Tenant** is the tenant namespace where the daemon set will be deployed.&#x20;
*   **Deployment Type** is either a DaemonSet, meaning Kubernetes, or Docker Native for built-in container orchestration.\


    <figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>The <strong>Update Security Agent Deployment</strong> page</p></figcaption></figure>



Once deployed, you can view the deployed instances of the agents under their respective agent tabs, as shown below:

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>The <strong>Agents</strong> page in the DuploCloud Portal</p></figcaption></figure>
