# Central Logging Setup

Setup of Central Logging comprises of two steps or components

**Control Plane:** This comprises of Open search and Kibana which are deployed in Default tenant.  An administrator can view these under Devops-->Containers-->EkS/Native. These are deployed just like any other application.

{% hint style="info" %}
Central Logging is disabled by default. It can be enabled from under Administrator --> Diagnostics --> Central Logging.
{% endhint %}

![](<../../../.gitbook/assets/image (5).png>)

**Log Collector:** Under each tenant a file beat service is deployed with the replica count equal to the number of hosts. If the number if hosts change, the platform will automatically adjust the replica count to match this. This is achieved by marking the service as a "DaemonSet". &#x20;

{% hint style="info" %}
After the Control plane has been deployed and is active, logging per tenant has to be enabled as well. Only then will the log collector (File Beat) be deployed. This can be done from under Administrator --> Diagnostics --> Settings and at the bottom of the page you see the option to enable Tenant logging.
{% endhint %}

![](<../../../.gitbook/assets/image (15).png>)

You can see these filebeat containers running within the tenant from under Devops --> Containers -->EKS/Native.&#x20;

### **Behind the Scenes**

Following orchestration steps were performed behind the scenes:

1. **Control plane deployment**:
   1. _**Add Hosts:**_ The platform added an Ec2 instance under the default tenant. This Host is typically called duploservices-default-oc-diagnostics.
   2. _**Added 2 services**_, under default tenant, one for open-search and other for Kibana. They were both pinned to the host added above using [allocation-tags](../../container-deployments/concepts.md). The Kibana was setup to point to this elastic Search. The kibana was exposed via an internal load balancer
   3. _**Security rules**_ from within the internal network to port 443 were added under the default tenant to allow the log collectors that will run on Tenant hosts to send logs to the elastic search. &#x20;
2. &#x20;**Log Collector**: The file beat setup comprises of a service called [filebeat-duploinfrasvc](https://radiant-dev.duplocloud.net/app/devops/c3b2f2dc-9b6b-4553-9c4e-19609f6289ed/containers/eks-native/services/filebeat-duploinfrasvc) deployed for each tenant where the central logging in enabled. The service configuration includes mounting the /var/lib/docker/Containers from the host into the filebeat container. The filebeat container is pointing to the elastic search running in default tenant. Inside the container the file beat has been setup in such a way that each log line is added with the meta-data information comprising of Tenant Name, Service Names, Container ID and Host Name. Thus inside the elastic search it is easy to separate the logs by these parameters  &#x20;
