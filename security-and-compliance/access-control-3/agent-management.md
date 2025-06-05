---
description: >-
  Setup and management of agents such as OSSEC, ClamAV for anti-virus,
  CrowdStrike, and so forth
---

# Agent Management

Security agents monitor virtual machines for threats, vulnerabilities, and compliance. They collect security-related data and send it to centralized controlling software. Security agents include tools like OSSEC (used with SIEM Wazuh), ClamAV (anti-virus), CrowdStrike, and Lacework.&#x20;

DuploCloud provides seamless installation and management of these security agents, offering three types:

**1. Docker-based Agents**

These agents run as containers orchestrated by DuploCloud, with privileged access over the Host operating system. They can be deployed on all or a subset of hosts within a cluster.

**2. Kubernetes DaemonSet Agents**

Kubernetes DaemonSets ensure that security agents are deployed across all or a subset of Hosts in the cluster, typically with privileged access over the Host operating system.

**3. Non-Docker VM Agents**

These agents are Linux packages or Windows services installed on virtual machines, either baked into the VM image before launch or installed via user data scripts.

{% hint style="info" %}
**Security agents** focus on system protection and compliance, while **observability agents** monitor application performance, health, and infrastructure metrics. For more information on **observability agents**, please refer to the [observability documentation](../../diagnostics-overview/).
{% endhint %}

## Agent Registration

1.  **Create an Agent Type.** Each vendor or agent software is considered a type. For example, OSSEC, ClamAV, Laceworks, and Crowdstrike are different agent types. To add a new agent type, navigate to **Security** -> **Agents** and click **Add.** The **Add Security Agent** pane displays. Enter the **Agent Name** and click **Create**.\


    <div align="left"><figure><img src="../../.gitbook/assets/image (8) (2).png" alt=""><figcaption><p><strong>Add Security Agent</strong> pane.</p></figcaption></figure></div>
2. **Create an agent deployment.** Under the desired **Agent** tab, **Add** a deployment to deploy the agent to the Hosts. You must deploy at least one agent per Kubernetes cluster. You can deploy on all hosts in a Kubernetes cluster or on all Hosts for a specific Tenant. Deploying on all hosts for one Tenant is useful for certain Kubernetes clusters or DuploCloud Infrastructures where you have Tenants on which you don't want specific agents to be run.&#x20;

{% hint style="info" %}
Behind the scenes, this deployment is just a regular Kubernetes DaemonSet deployment or a built-in container orchestration deployment within a tenant, as documented here.&#x20;
{% endhint %}

## Creating multiple deployments for multiple Tenants&#x20;

You can create multiple deployments for multiple tenants. In the case of Kubernetes-based container orchestration, as against DuploCloud built-in orchestration, you can target all nodes in the cluster with just one deployment. The following are the fields in the **Update Security Agent Deployment** page:

* **Name** is a desired name to track the deployment.
* **Cluster** is the infrastructure name and is the maximum scope of deployment.&#x20;
* **Host Tenant** is the tenant namespace where the daemon set will be deployed.&#x20;
*   **Deployment Type** is either a K8s DaemonSet or Docker Native for built-in container orchestration.\


    <figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>The <strong>Update Security Agent Deployment</strong> page</p></figcaption></figure>



Once deployed, you can view the deployed instances of the agents under their respective agent tabs, as shown below:

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption><p>The <strong>Agents</strong> page in the DuploCloud Portal</p></figcaption></figure>
