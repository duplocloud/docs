---
description: >-
  Setup and management of agents such as OSSEC, ClamAV for anti-virus,
  CrowdStrike, and so forth, focusing on both observability and security aspects.
---

# Agent Management

Agents are typically required to be installed on virtual machines to collect data and send it to their respective controlling software running in a central location. For example, OSSEC is the agent for the SIEM Wazuh. CrowdStrike and Laceworks all have their respective agents. ClamAV anti-virus can also be considered an agent whose results we collect and send to Wazuh.

DuploCloud platform provides seamless installation and management of these agents, distinguishing between Observability Agents, managed by DevOps for operational performance, and Security Agents, overseen by SecOps focusing on security and compliance. This distinction ensures that the right team manages the appropriate aspects of application management, with a security admin role specifically designed for accessing and managing security operations.

There are 3 types of agents that we install:

* Docker-based agents
  * The Kubernetes DaemonSet runs in all or a subset of hosts in a cluster. Typically, these containers are launched with privileged access over the host operating system.
  * Containers that run on all or a subset of hosts are orchestrated through DuploCloud's built-in container orchestration. Typically, these containers are launched with predefined access to the host operating system.
* Non-Docker VM agents are Linux packages or Windows services installed and baked into virtual machine images before launch. They can also be installed via user data.

## Agent Setup

1.  **Create an Agent Type.** Each vendor or agent software is considered a type. For example, OSSEC, ClamAV, Laceworks, and Crowdstrike are different agent types. To add a new agent type, navigate to **Security** -> **Agents** and click **Add.** The **Add Security Agent** pane displays. Enter the **Agent Name** and click **Create**.

    <figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p><strong>Add Security Agent</strong> pane.</p></figcaption></figure>

2. **Create an agent deployment.** Under the desired **Agent** tab, **Add** a deployment to deploy the agent to the Hosts. You must deploy at least one agent per Kubernetes cluster. You can deploy on all hosts in a Kubernetes cluster or on all Hosts for a specific Tenant. Deploying on all hosts for one Tenant is useful for certain Kubernetes clusters or DuploCloud Infrastructures where you have Tenants on which you don't want specific agents to be run.

{% hint style="info" %}
Behind the scenes, this deployment is just a regular Kubernetes DaemonSet deployment or a built-in container orchestration deployment within a tenant, as documented here.
{% endhint %}

### Understanding Virus Scan Scope

When deploying or managing containers and cloud services, it is essential to ensure the security and integrity of your systems. Virus scans play a crucial role in this process by checking for malicious software, vulnerabilities, and any security threats within the defined scope. This includes all areas and items the virus scanning process covers during its operation, ensuring the safety of your network and systems.

## Creating multiple deployments for multiple Tenants

You can create multiple deployments for multiple tenants. In the case of Kubernetes-based container orchestration, as against DuploCloud built-in orchestration, you can target all nodes in the cluster with just one deployment. The following are the fields in the **Update Security Agent Deployment** page:

* **Name** is a desired name to track the deployment.
* **Cluster** is the infrastructure name and is the maximum scope of deployment.
* **Host Tenant** is the tenant namespace where the daemon set will be deployed.
*   **Deployment Type** is either a K8s DaemonSet or Docker Native for built-in container orchestration.

    <figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>The <strong>Update Security Agent Deployment</strong> page</p></figcaption></figure>

Once deployed, you can view the deployed instances of the agents under their respective agent tabs, as shown below:

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption><p>The <strong>Agents</strong> page in the DuploCloud Portal</p></figcaption></figure>

This clear division of responsibilities between DevOps and SecOps within the DuploCloud UI ensures that both operational performance and security compliance are efficiently managed, reflecting the platform's commitment to providing comprehensive agent management capabilities.