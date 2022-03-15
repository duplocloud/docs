# Application Requirements

The application engineers  start off by giving a set of requirements to the operations or DevOps team. This typically includes:&#x20;

1. **High level architecture.** Like the example shown in the figure below which depicts the following: \
   \- A set of docker containers to be deployed connected to a SQL database along with a Redis instance and an S3 bucket. \
   \- Part of the containers needs to be behind a public ELB, part behind an internal LB.  \
   \- Data science team may want a Spark cluster connected to ES \
   \- Lambda functions behind API gateway are to be deployed. &#x20;

![High Level Engineering Requirements](<../.gitbook/assets/Screen Shot 2022-03-12 at 1.08.33 PM.png>)

2\. **Multiple environments** might be required: Dev, Stage, QA and Production. In some case there may be a need to deploy a unique copy of the application for each customer (Single Tenant Application). &#x20;

3\. **Diagnostics.** Central logging, monitoring and alerting must be established.&#x20;

4\. **Compliance standards.** Specific standards are to be met like PCI, HIPAA, SOC 2 etc.&#x20;

5\. **CI/CD** is to be established.&#x20;
