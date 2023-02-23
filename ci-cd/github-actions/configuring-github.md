---
description: This section discusses how you can configure Github to integrate with Duplo
---

# Configuring GitHub

In order to call a DuploCloud API from Github, you will need to obtain an API token.

{% content-ref url="../../../administrators/access-control/api-tokens.md" %}
[api-tokens.md](../../../administrators/access-control/api-tokens.md)
{% endcontent-ref %}

The basic steps are:

1. **(Recommended)** Create a "service account" user in DuploCloud that will own the API token.
2. Give the DuploCloud user access the desired tenant. See [adding tenants to a user](../../../administrators/access-control/tenant-access.md#adding-tenant-access-for-a-user).
3. Create an API token for that user. See [creating API Tokens](../../../administrators/access-control/api-tokens.md).
4. Add a Github Repository secret that contains the DuploCloud API token.&#x20;

{% hint style="info" %}
**Note:** A 'service account' user in DuploCloud is just a user whose user name is not an email address, such as `github-bot` or `my-api-user`. These users are not able to log in.
{% endhint %}

{% content-ref url="../../../administrators/access-control/tenant-access.md" %}
[tenant-access.md](../../../administrators/access-control/tenant-access.md)
{% endcontent-ref %}

![](<../../../.gitbook/assets/Screen Shot 2022-02-24 at 2.32.57 PM.png>)

{% hint style="warning" %}
The rest of this documentation will assume that you named the github repository secret `DUPLO_TOKEN`.
{% endhint %}
