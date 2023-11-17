# API tokens

## Introduction

Duplo supports two kinds of API tokens, temporary API tokens and permanent API tokens. For normal use cases, we recommend using a temporary API token. For CI/CD or other DevOps automation, a permanent API token is warranted.

{% hint style="warning" %}
Permanent API tokens will expire after one year.
{% endhint %}

## Temporary API tokens

Every time a user logs in to Duplo, a temporary API token is created for that user that only lasts for the duration of their session.

### Getting a Temporary API token

Any user can retrieve _their own_ temporary API token from Duplo. Navigate to the **User -> Profile** page. Click the copy icon ![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.19.23 PM.png>) in the **Temporary API Token** pane

![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.16.50 PM.png>)

## Permanent API tokens

Only administrators can create permanent API tokens. Permanent tokens are always associated with a specific Duplo user.&#x20;

{% hint style="warning" %}
**Note:** Permanent API tokens will expire after one year.
{% endhint %}

### Creating a permanent API token

Navigate to the **Administrator -> Users** page. Click the username in the list, to go to a specific user's page. Click the **Tokens** tab.

![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.26.24 PM.png>)

Click the blue **+ Add** button. Give your token a memorable name and click **Create**.

![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.27.12 PM.png>)

Click the **Copy** button to copy your token to the clipboard.  Save it somewhere safe, you will not be able to retrieve it from Duplo later.

![](<../../.gitbook/assets/Screen Shot 2022-02-24 at 2.29.53 PM.png>)

{% hint style="danger" %}
**Caution:** Always save your token somewhere safe. You will not be able to retrieve it again from Duplo after you have created it. However, if you lose your token, you can always create a new one.
{% endhint %}
