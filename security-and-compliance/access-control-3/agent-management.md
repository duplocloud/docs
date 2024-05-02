# Agent Management

Agent is a software that is typically required to be installed on the virtual machines so they can collect data and send to their respective controlling software running in a central location. For example ossec is the agent for the SIEM Wazuh. Crowdstrike, laceworks all have their respective agents. ClamAv anti virus can also be considered an agent whose results we collect and send to Wazuh.

DuploCloud platform provides seamless installation and management of these agents. There are 3 types of agents that we install:

* Docker based agents
  * Kubernetes DaemonSet and runs in all or a subset of hosts in a cluster. Typically these containers are launched with previliged access over the host operating system
  * Containers that run on in all or a subset of hosts being orchestrated through DuploCloud's [built-in container orchestration.](../../container-deployments/container-orchestrators.md) Typically these containers are launched with previliged access over the host operating system.
* Non-Docker VM agents are linux packages or windows services that are installed and baked in virtual machine images before they are launched. They can also be installed via user data. &#x20;

Agent installation menu is under Security->Agents. There are 2 steps in the agent setup:

*   **Create an Agent Type**: Each unique vendor or agent software can be considered a type. For example ossec, clamav, laceworks, crowdstrike are all different agent types. To add a new agent type, under Security -> Agents click on + and it requires only a name as shown below.\


    <figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>


* **Create an agent deployment:** Under the desired agent tab add a deployment which will deploy the agent to the hosts. You need to create at least one deployment per kubernetes cluster. There are a few deployment options:
  * Deploy on all hosts in the kubernetes cluster
  * Deploy on all hosts only for a certain tenant. This would be a use case where in a certain cluster/DuploCloud infrastructure you  have some tenants where you don't want these agents to be in.&#x20;

{% hint style="info" %}
Behind the scenes this deployment is just a regular Kubernetes Daemonset deployment or a built-in container orchestration deployment within a tenant as documented here.&#x20;
{% endhint %}

&#x20;\
You can create multiple deployments for multiple tenants. In case of Kubernetes based container orchestration as against Duplocloud built-in orchestration, with just one deployment you can target all nodes in the cluster. Following are the elements of the deployment menu:

* Name is a desired name to track the deployment.
* Cluster is the infrastructure name and is the maximum scope of deployment.&#x20;
* Host Tenant is the tenant namespace where the daemon set will be deployed.&#x20;
*   Deployment type is either DaemonSet meaning kubernetes or Docker Native for built-in container orchestration.\


    <figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>



Once deployed you can view the deployed instances of the agents under the respective agent tab as shown in picture below

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>
