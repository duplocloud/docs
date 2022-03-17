# ACM Certificate

DuploCloud platform needs a wild char ACM certificate corresponding to the domain that was created. For example if the Route 53 hosted zone created was apps.acme.com then the certificate will be for \*.apps.acme.com You can also choose to add more domains to this certificate for example \*.acme.com

This certificate is used to apply on ELBs that are created as part of application deployment later. Follow this AWS guide to issue an certificate [https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html#request-public-console](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html#request-public-console)

Once the certificate is issued we need to set the ARN of the certificate in the DuploCloud Plan so that they are available to the subsequent configurations. In DuploCloud start by setting this in default plan. To Do so, go to Administration --> Plans -->Default --> Certificates and click on Add. Give a friendly name and give the arn.

{% hint style="info" %}
Note that this certificate has to be set in every new plan created as part of the infrastructure
{% endhint %}
