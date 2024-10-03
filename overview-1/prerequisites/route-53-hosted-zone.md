---
description: Creating a Route 53 hosted zone to program DNS entries
---

# Cloud DNS Zone

The DuploCloud platform needs a unique GCP Cloud DNS zone to create DNS entries for services that you deploy. The domain must be created out-of-band and set in DuploCloud. The zone is a subdomain such as `apps.[`_`MY-COMPANY`_`].com or internal.[my-company]`.com&#x20;

{% hint style="danger" %}
**Never use this subdomain for anything else, as DuploCloud owns all `CNAME` entries in this domain and removes all entries it has no record of.**
{% endhint %}

To create the hosted zone using the GCP Console:

1. Log in to the [GCP console](http://console.cloud.google.com/).
2. Navigate to **Cloud DNS** under **Network Services**.&#x20;
3. Click on "Create Zone" as shown in the picture below and note down the **Zone name** that you have created as this will be required to be added into DuploCloud later: \
   ![](<../../.gitbook/assets/image (3).png>)![](<../../.gitbook/assets/image (1) (1) (1).png>)
4. Access the zone and note the [name server](https://docs.aws.amazon.com/Route53/latest/APIReference/API\_domains\_Nameserver.html) names.
5. Go to your root Domain Provider's site (for `acme.com`, for example), and create a `NS` record that references the domain name of the hosted zone you created (`apps.acme.com`) and add the zone name to the name servers that you noted above.

Once this is complete, provision the Zone in every DuploCloud Plan, starting with the plan we just created in the previous step. Add the zone Name and domain name, preceded with a dot (**.**).

{% hint style="warning" %}
Do not forget the dot (**.**) at the beginning of the DNS suffix, in the form as shown below.
{% endhint %}

<div align="left">

<figure><img src="../../.gitbook/assets/image (314).png" alt=""><figcaption></figcaption></figure>

</div>

{% hint style="info" %}
Note that this domain must be set in each new Plan you create in your DuploCloud Infrastructure.
{% endhint %}
