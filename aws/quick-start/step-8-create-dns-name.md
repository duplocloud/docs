# Step 8: Create DNS Name

Once the load balancer has been provisioned, DuploCloud by default create a DNS name for the service and programs it in the Route53 domain that was created as part of the [pre-requisites](../prerequisites/route-53-hosted-zone.md) The default name for the service will be \<servicename>-\<tenantname>.\<Dnssubdomain> where the DNS subdomain is the domain configured as part of the [pre-requisites](../prerequisites/route-53-hosted-zone.md)

{% hint style="info" %}
It can take as long as 10-15 minutes for the DNS to be active. You can try to connect using the internal AWS Load balancer DNS name like elb.amazonaws.com but it will give a certificate error that can be ignored.
{% endhint %}

You can change this under Devops-->Containers-->EKS/Native-->\<ServiceName>-->LoadBalancers and the first card in that tab as shown in the picture below.

&#x20;                                            &#x20;

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

