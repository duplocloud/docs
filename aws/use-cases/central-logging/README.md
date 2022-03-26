# Central logging

DuploCloud platform comes with an option of centralized logging for Docker based applications. For the built-in and Kubernetes container orchestration this is implemented using OpenSearch and Kibana with filebeat as the log collector. For ECS fargate, AWS Lambda and Sage Maker Jobs, the platform integrates with CloudWatch setting up automatically Log Groups and making them viewable from the DuploCloud Portal.

{% hint style="info" %}
No setup is required to enable logging for ECS Fargate, Lambda or Sage Maker Jobs. The platform automatically sets up CloudWatch log groups and gives easy to access menu next to the resource.&#x20;
{% endhint %}





&#x20;
