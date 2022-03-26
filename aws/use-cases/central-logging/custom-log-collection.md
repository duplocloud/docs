# Custom Log Collection

There are several use cases for customized log collection. Since the entire central logging stack is deployed within your own environment just like any other application, we are allowed to make customizations easily.

* **Control Plane Configuration changes** like Open search version, EC2 host size, : The control plane configuration deployed is based off the configuration defined in Administrator --> System Settings --> Service Descriptions --> duplo\_svd\_logging\_opensearch. You can edit this. These edits allow you to change various parameters of the control plane deployment.

&#x20;

![](<../../../.gitbook/assets/image (21).png>)

{% hint style="info" %}
Note that these changes have to be done before enabling the central logging. If you already have the control plane deployed then making an update is like making a change to any other application. In this case the control plane components are deployed under default tenant. Where you can directly make changes like increasing instance size, change docker images etc
{% endhint %}
