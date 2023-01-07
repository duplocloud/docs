# Quick Start - DuploCloud Docker Services

This tutorial shows you how to setup an end-to-end cloud deployment for the sample topology&#x20;

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* We will use simple Nginx web as a sample for the application container.
* We will use the Tenant and Infrastructure created as part of [Step1](../step-1-infrastructure.md) and [Step2](../step-2-tenant.md).
* We will deploy the docker containers by leveraging DuploCloud platform in-built container management capability

Following will be DuploCloud mapping of the above topology into DuploCloud constructs. The steps involved in the setup will be:

1. Use the Infrastructure created at Step1 and Step2 in the quickstart guide.
2. Create a Host (EC2 Instance)&#x20;
3. Create a micro-service called webapp with the docker image as nginx:latest
4. Expose the webapp using a loadbalancer and a DNS name. Test it.
