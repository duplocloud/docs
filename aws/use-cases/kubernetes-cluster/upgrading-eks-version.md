# Upgrading EKS version

AWS frequently updates the version of EKS based on new features being available in the Kubernetes platform. DuploCloud allows this upgrade to be automated through the UI.

**IMPORTANT: EKS version upgrade could cause downtime to your application depending on the number of replicas you have configured for your services. To be safe, this upgrade should be scheduled outside of business hours.**

### Upgrade Process

At a high level, the process involves:

* Updating EKS Control Plane to the new version
* Re-launch all hosts to deploy the new version on all nodes.
* Apply allocation tags to hosts if needed.

### Starting the Upgrade&#x20;

Goto **Administrator->Infrastructure**, click into the Infrastructure where the **EKS** cluster, and then goto EKS tab, it should show something like below:

![](<../../../.gitbook/assets/Screen Shot 2022-07-16 at 4.54.35 PM.png>)

### Monitoring the Upgrade&#x20;

Clicking on Upgrade will start the process and it shows a step by step progress on the Upgrade.

![](<../../../.gitbook/assets/Screen Shot 2022-07-16 at 4.58.59 PM.png>)

### Upgrade Completion

The above screen should show progress through all incremental updates through the versions and all hosts that needs an upgrade should be replaced. You should get a all GREEN checkmark on the checklist status list.

### Apply Allocation Tags

If any of your hosts used allocation tags, you will have to assign allocation tags to the hosts, as they get online, manually by going to **DevOps->Hosts** and edit the allocation tag for each of the hosts. There is a product improvement planned to make this automated

&#x20;                                     <img src="../../../.gitbook/assets/Screen Shot 2022-07-16 at 5.03.32 PM.png" alt="" data-size="original">



