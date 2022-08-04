# Custom Log Collection

There are several use cases for customized log collection. Since the entire central logging stack is deployed within your own environment just like any other application, we are allowed to make customizations easily.

* **Control Plane Configuration changes** like Open search version, EC2 host size, : The control plane configuration deployed is based off the configuration defined in Administrator --> System Settings --> Service Descriptions --> duplo\_svd\_logging\_opensearch. You can edit this. These edits allow you to change various parameters of the control plane deployment.

&#x20;

![](<../../../.gitbook/assets/image (21) (1) (1) (1).png>)

{% hint style="info" %}
Note that these changes have to be done before enabling the central logging. If you already have the control plane deployed then making an update is like making a change to any other application. In this case the control plane components are deployed under default tenant. Where you can directly make changes like increasing instance size, change docker images etc
{% endhint %}

* **Log Collector Customization:** At times there may be customizations required in the file beat configurations. This includes configuration like mounting different folder than just /var/lib/docker because the application may be writing logs in a different folder that just doing stdout. To make these changes you need to edit Administrator --> System Settings --> PlatformServices and pick the filebeat versions. There are two versions one for Kubernetes based and one for Native Container Management based. \


{% hint style="info" %}
Note that these changes have to be done before enabling the logging for the tenant. If you already have the log collector deployed then you either make an update to the filebeat configuration in each tenant by editing the filebeat service. Another simple way is you can delete the filebeat collector from the Tenant and the platform will automatically redeploy based on latest configuration.&#x20;
{% endhint %}

* **Third Party Logging Tools:** Another common use case is to use tools like datadog, sumologic etc. This is rather agnostic to the DuploCloud platform. Typically users would deploy Docker containers that act as collectors and agents from these tools. Deployment of these containers is like any other application service.&#x20;
