# Agent Management

Agent is a software that is typically required to be installed on the virtual machines so they can collect data and send to their respective controlling software running in a central location. For example ossec is the agent for the SIEM Wazuh. Crowdstrike, laceworks all have their respective agents. ClamAv anti virus can also be considered an agent whose results we collect and send to Wazuh.

DuploCloud platform provides seamless installation and management of these agents. There are 3 types of agents that we install:

* Docker based agents
  * Kubernetes DaemonSet and runs in all or a subset of hosts in a cluster. Typically these containers are launched with previliged access over the host operating system
  * Containers that run on in all or a subset of hosts being orchestrated through DuploCloud's [built-in container orchestration.](../../container-deployments/container-orchestrators.md) Typically these containers are launched with previliged access over the host operating system.
* Non-Docker VM agents are linux packages or windows services that are installed and baked in virtual machine images before they are launched. They can also be installed via user data. &#x20;

Agent installation menu is under Security->Agents. There are 2 terms to be aware of:

* Agent Type: each unique vendor or agent software can be considered a category. For example ossec, clamav, laceworks, crowdstrike are all different agent types.
