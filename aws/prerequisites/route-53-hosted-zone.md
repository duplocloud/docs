---
description: Creating a Route 53 hosted zone to program DNS entries
---

# Route 53 Hosted Zone

The DuploCloud platform needs a unique route 53-hosted zone to program DNS entries for services that you deploy. The domain must be created out-of-band and set in DuploCloud. The zone is a subdomain such as `apps.[`_`MY-COMPANY`_`].com`.&#x20;

{% hint style="danger" %}
**Never use this subdomain for anything else, as DuploCloud owns all `CNAME` entries in this domain and removes anything entries it has no record of.**
{% endhint %}

To create the Route53 hosted zone using the AWS Console:

1. Log in to the [AWS console](https://aws.amazon.com/console/).
2. Navigate to **Route 53 and Hosted Zones**.&#x20;
3. Create a new hosted zone with the desired domain name, for example, `apps.acme.com`.&#x20;
4. Access the hosted zone and note the [name server](https://docs.aws.amazon.com/Route53/latest/APIReference/API\_domains\_Nameserver.html) names.
5. Go to your root Domain Provider's site (for `acme.com`, for example), and create a `NS` record that references the domain name of the hosted zone you created (`apps.acme.com`) and add the zone name to the name servers that you noted above.

Once this is complete, provision the Route53 domain in every DuploCloud Plan, starting with the **default** plan. Add the Route53 hosted zone ID and domain name, preceded with a dot (**.**).

{% hint style="warning" %}
Do not forget the dot (**.**) at the beginning of the DNS suffix, in the form as shown below.
{% endhint %}

![DNS tab for DEFAULT tenant with External/Internal Suffix Values beginning with a dor (.)](<../../.gitbook/assets/image (18) (2).png>)

{% hint style="info" %}
Note that this domain must be set in each new Plan you create in your DuploCloud Infrastructure.
{% endhint %}
