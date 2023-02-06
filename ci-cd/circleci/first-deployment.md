# First Deployment

## Introduction

Before using CI/CD, the first deployment of the application needs to be done via DuploCloud menus described above. Make sure that the application works as expected. CircleCI Actions is recommended to be used only for upgrades of container images and to run tests that can be written to run before and after.

## Create API tokens

1. **(Recommended)** Create a "service account" user in DuploCloud that will own the API token.
2. Give the DuploCloud user access the desired tenant. See [adding tenants to a user](../../administrator-tools/access-control/tenant-access.md#adding-tenant-access-for-a-user).
3. Create an API token for that user. See [creating API Tokens](../../administrator-tools/access-control/api-tokens.md).
4. Add a Github Repository secret that contains the DuploCloud API token.

{% hint style="info" %}
**Note:** A 'service account' user in DuploCloud is just a user whose user name is not an email address, such as `github-bot` or `my-api-user`. These users are not able to log in
{% endhint %}

{% content-ref url="../../administrator-tools/access-control/tenant-access.md" %}
[tenant-access.md](../../administrator-tools/access-control/tenant-access.md)
{% endcontent-ref %}

## Add token at context level

1. Login to CircleCI portal and click on "Organization Settings" in the left hand sidebar
2. Click on "Create Context" button and create one by providing name for your context.
3. Click on the newly created context and scroll to "Environment Variables" section.
4. Click on "Add Environment Variable" and enter the variable name "DUPLO\_TOKEN" and value as token created in above steps.
5. Click on "Add Environment Variable".
6. Add the one more variable with name as "DUPLO\_HOST" and value as DuploCloud portal URL.
